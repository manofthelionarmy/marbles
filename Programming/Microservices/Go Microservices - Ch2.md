[Links?](#)
[Go Code Review Comments - Laundry List of Common Style Issues](https://github.com/golang/go/wiki/CodeReviewComments)
[Effective Go - Tips for Writing Idiomatic Go](https://go.dev/doc/effective_go)
[Tips on Package Names](https://go.dev/blog/package-names)
[Book's Source Code](https://github.com/PacktPublishing/Microservices-with-Go/tree/08c6285e9c9c4b459ac7f094eee028f63665e9e6)
[Layered Architecture](https://www.baeldung.com/cs/layered-architecture)
[Embbed Videos?](#)
# Summary

----
# Related Stuff
[[Golang Project Layout]]
#golang 
#microservices 

----
# Notes:
### 2023-05-08:
- This goes over 3 things:
	- Go basics
	- Project Structure
	- Scaffolding an example application
- By Go basics, the author is not referring to syntax or fundamentals of the go language.
	- Instead, it focues on standard advice or principles:
		- Always follow the official guidelines
		- Follow the style used in the standard library
		- Do not try to apply the ideas from other languages to Go
			- Tbh, I don't know much about this. I'm not sure what other ideas of other programming languages may not fit into Go.
- Other basics the author refers to is writing idiomatic Go Code.
	- This is better covered in *100 Go Mistakes*.
- The last tip is on project structure or scaffolding, and distingues between `internal`, `pkg`, and `cmd`. All of which can be found in [[Golang Project Layout]]
- Again, project scaffolding is better covered in *100 Go Mistakes*.
#### 06:53pm:
- I implemented the `metadata` microservie by following along the code listed in the github. The code listed in the e-book in O'reilly wasn't fully visible, hence why I went to the source code.
- The design of the `metadata` microservice uses a *Layered Architecture* or *N-tiered* architecture.
- The layers in this book are the `controller`, `handler`, and `respository`
	- I tried looking online, this pattern feels familiar, like the ones used in SpringBoot.
	- It appears to be used in .Net too: 
		- [Repository Service Pattern](https://exceptionnotfound.net/the-repository-service-pattern-with-dependency-injection-and-asp-net-core/)
		- In the diagarm, it does include controller, but doesn't include any details what it is.
- I looked up *Rest Controller*:
	- [Rest Controller - Geeks For Geeks](https://www.geeksforgeeks.org/spring-rest-controller/)
	- It looks like this pattern and the pattern in the book match. The REST controller just maps routes to a handler. 
- However, we have `http` which calls the `controller` logic. It routes the request to a handler and we pass the data to the `controller`, which may controll business/application logic and uses the `repository` layer.
- When I implemented the rating and movie pattern, it had the same  patterns: a layered architecture with controller and repository. Apart from rating and metadata services, movie service has a `Gateway` layer, which just encapsualtes how a client will make requests to the `rating` and `metadata` service. This makes sense, what if we implement our `rating` and `metadata` service as gRPC servers or JSON RPC servers. Then our client implementation has to be different.
- I think I found a repo that kind of explains some of the abstracted elements in this book. By kind of, I mean it includes most of them except the `Gateway`: 
	- https://github.com/irahardianto/service-pattern-go
- A side note, I like how the author tries to point out not to try and fit other idomatic stuff for other languages in go, and a lot of this stuff looks familiar to Java. Go isn't object oriented, but it does use interfaces.
- There's another pattern, hexigonal architecture, which I want to review. It uses a service-repository pattern. It is also known as the `Ports and Adapaters` pattern. It got name "hexagonal" because they used a hexagon in the diagram to fit all abstracted components in it. It has nothing to do with having 6 ports or adapters.
- Though we have our http logic, I find it kind of redundant we have a struct called `Handler` and it's a wrapper of `Controller`. This composition is moreso of an aggregation because it uses Controller as a service. However, we are creating http handlers, which we have to pass in as arguments for our server mux for routing. Handlers, pretty much do the *controller* logic. It controls what will happen to the request, or handles the request and produces a response. Maybe it wouldn't been better to name `Controller` as `Service`.
- This is how that one repo defines a `Service`: 
> services is where the business logic lies on, it handles controller request and fetch data from data layer it needs and run their logic to satisfy what controller expect the service to return.
- According to this logic:
  https://github.com/irahardianto/service-pattern-go/blob/master/controllers/PlayerController.go
  - It looks like like the Controller ***is*** the handler. And it wraps around the `Service`.
- The difference in the book, it uses `Handler` in place of `Controller` and `Controller` in place of Service.
- A bit weird, I don't agree with the author's approach, yet again, there's a lot of freedom in go and there's never a right answer how to design a project.
## Questions:

## Follow Up:
- Review project scaffolding in *100 Go Mistakes* and Hexagonal Architecture.
- Make the links into their own pages.
- May have to implement code in chatper 2. I guess it continues off with the code example from chapter 2 into chatper 3.
