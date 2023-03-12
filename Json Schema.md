
 [JSON at work](https://www.amazon.com/JSON-Work-Practical-Data-Integration/dp/1449358322)
# Summary:
- JSON Schema has its own specification and it allows us to validate a payload that is sent to our server. 
- This helps us develop a contract for our API, which is an interface to our applicaiton.
---
# Related Stuff:
 [[An Architect's Guide to APIs - SOAP, REST, GraphQL, and gRPC]]
[[Hypermedia]] 

 #golang 
 #nodejs 
 
---
# Notes:
- JSON is javascript object notation, and its the data format that can be used by HTTP and the REST, RPC, and GraphQL api paradigms.
- JSON has its own specification for it's data represenation, that being objects, name/value pairs, and arrays.
- Though JSON can be used to model our data, how do we validate it against the established schema for our projects.
- Json Schema defines the structure ("shape") of our json payloads. We can use a json schema processor to validate incoming requests. By that, I mean we are checking if they follow api design and it's interface, and that is why books have said it's like a API contract.
- A weird analogy I think of is that say we defined an interface in golang. And we try to pass a struct that doesn't implement the interface to function that has the interface as an argument. The compiler will catch that, and an error is thrown. Or, it will be caught at runtime too and a panic will occur. In other words, there is some validation if something is following or respecting the interface.
	- Continuing with the analogy, when you create your api or rest endpoints, there is nothing barring the reqeusts from following your intended api. For example, you may be expecting a certain payload to be passed to your REST endpoint, but you get one that doens't match at all. You can write a bunch of `if/else` statements, but you can't catch all of the edge cases. It's better to use a JSON schema (and I'm assuming the json schema processor works as some middleware).
 - Json Schema has a specification that defines the core types, basic types, constraints for more fine-grained validation (such as conditions like max lenghth for a string value, a range for numerical values, exclusive matching for conditions, etc.), support for internal and external dependencies via internal and external references.
## Follow Up: 
- What is OpenAPI (Swagger) specification?
	- <mark style="background: #FFB86CA6;">Read the book Designing APIs with Swagger and OpenAPI by Josh Ponelat.</mark>
- What is Hypermedia format?
	- It was mentioned in this book: *JSON at Work* by Tom Marrs.
	 - *RESTful Web APIS* by Leonard Richardson (O'reilly) goes more over this topic, and I assume implementation.
	  - REST in Practice: Hypermedia and Systems Architecture, by Jim Webber (O'reilly)
- Can you use OpenAPI and JSON Schema together?
	- This article gives tips on how they can:
		- [Open API and JSON Schema: When to Use Which](https://blog.stoplight.io/openapi-json-schema)
  