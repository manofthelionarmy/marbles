[Routers - MDN](https://developer.mozilla.org/en-US/docs/Glossary/routers)
[Chi - golang](https://github.com/go-chi/chi)
# Summary:
# Related Stuff:
[[Section 2 - Building a Simple Frontend and Broker Service]]
[[Express - Routers Object]]
#webapplications
#golang 
#express 
#nodejs 

# Notes:
> In the implementation of an [API](https://developer.mozilla.org/en-US/docs/Glossary/API) in a service layer, a router is a software component that <mark style="background: #FFB86CA6;">parses a request and directs or routes the request to various handlers</mark> within a program. The router code usually <mark style="background: #FFB86CA6;">accepts a response from the handler and facilitates its return to the requester</mark>.

- Golang has standard library support for http, but not for routing. Fortunately, there are packages where this is solved. A popular one is `gorilla/mux` another one is `chi`, which is a lightweigth router.
	- We use `chi` in the udemy course.