[Links?](#)
[Embbed Videos?](#)
[Sync Pool](https://pkg.go.dev/sync#Pool)
[Sync Pool Leads to Performance Improvement](https://www.akshaydeo.com/blog/2017/12/23/How-did-I-improve-latency-by-700-percent-using-syncPool/)
[Deep Analysis of Sync pool](https://www.sobyte.net/post/2022-03/think-in-sync-pool/)
# Summary
- `sync.Pool` is one way to prevent garbage collection to active more frequently. 
----
# Related Stuff
#golang 

----
# Notes:
- If we have temporary objects that haven't been used yet, and we want to cache them to lessen the number of times the garbage collector runs, we can use `sync.Pool`.
- Here, gin uses `sync.Pool`:
	- https://github.com/gin-gonic/gin/blob/master/gin.go#L165C6-L165C6
- It's a struct field of `Engine`. An engine implements `http.Handler`, so here, from: https://github.com/gin-gonic/gin/blob/master/gin.go#L570
```go
func (engine *Engine) ServeHTTP(w http.ResponseWriter, req *http.Request) {
	c := engine.pool.Get().(*Context)
	c.writermem.reset(w)
	c.Request = req
	c.reset()

	engine.handleHTTPRequest(c)

	engine.pool.Put(c)
}
```
- This article: https://www.sobyte.net/post/2022-03/think-in-sync-pool/ says that gin uses sync.Pool to reuse the gin.Context. Which we see above. This article also goes in depth.
- It appears gin is a http framework and the engine ensures we have an easy way of setting up routing and execute our middlewares. 
	- Remember middlewares validate our requests or even modifies data in them.
		- Hence, why we want to pass the request along. 
- ~~However, I have a concern, every time we handle a request, we get the gin context that was instantiated at the beginning of the program. Every time we perform a `pool.Get`, we are doing a memory lock and memory unlock. Now imagine if we are handling 1 million requests. Everytime we're at the route, we perform a `sync.Pool.Get`. Does this make all the goroutines go to sleep?~~ 
- Here is where the main handler `gin.Engine` runs:
	- https://github.com/gin-gonic/gin/blob/master/gin.go#L385
	- So, does `gin.Engine` work like `http.ServerMux`?
- How does a server mux work in golang? Does it handle goroutines per route? I can't remember.
	- I looked it up: https://github.com/golang/go/blob/08e39a196186b0b2ce852a156515001b8de190dc/src/net/http/server.go#L1999C1-L2007C46
- this is what the developers say:
```go
// HTTP cannot have multiple simultaneous active requests.[*]
		// Until the server replies to this request, it can't read another,
		// so we might as well run the handler in this goroutine.
		// [*] Not strictly true: HTTP pipelining. We could let them all process
		// in parallel even if their responses need to be serialized.
		// But we're not going to implement HTTP pipelining because it
		// was never deployed in the wild and the answer is HTTP/2.
		inFlightResponse = w
		serverHandler{c.server}.ServeHTTP(w, w.req)
```
- It looks like we concurrently handle requests, and can't return other ones until one request is returned. 
	- So this means the way gin uses sync.Pool doesn't really block other requests... from the `net/http` implementation, different goroutines are already blocked, meaning requests can't be served until one of them finishes.
- After reading the article that does an analysis on `sync.Pool`, it uses a complex data structure (a linked list of queues and each entry points to a head-tail ring buffer).
- Just know, per thread an entry is created when we call `sync.Pool.Put`. And when we call `sync.Pool.Get`, we the item and it's dequeued. 
- `sync.Pool` is concurrently safe without using mutexes.
- This is from the article that states how they uses `sync.Pool` to speed up their code:
> What if you pass a pooled object to a go-routine and submit it back to the pool before go-routine yet to complete the execution?
>
> This is a pickle, once you put back the object, it’s ready for reuse. So before you putting back the object inside the pool, you have to be sure that nothing else is using the same object for any other operation.
- According to this, once the item is dequeued, it's gone. 
- Also, entries are stolen from other threads. 
> Finally, if all the cache pools are out of data, the user-set New function is called to create a new object.
- this diagram does a good job at explaining this:
![[Pasted image 20231222193845.png]] 
- So, we get from local pool chain, else we still from others pool chain. If they haven't stored anything via `sync.Pool.Put`, we create a new object.
- I don't see how this helps with lowering the number of times the garbage collector is active.
	- I guess it depends on the ratio of invocations of `Gets` to `Puts` (i.e. the number of times each is called.) I also have to assume this is a empty struct value (one that hasn't been mutated.) I think that's why we reset it per go routine. We just want the struct value to be allocated in memory already, and we don't want the garbage collector to sweep it up. We want to cache it and keep the allocated memory and we don't care about what happened to the data.
- So that means in the gin requests being served, there will be times we return a new gin.Context, and one that has been allocated already in memory.
- The only way if a gin.Context has been added to the pool is if the request has completed and has been put in the pool, therefore `gin.Context.Request` is concurrently safe.
## Questions:

## Follow Up:
