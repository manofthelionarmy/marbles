[Express API - Routers](https://expressjs.com/en/4x/api.html#router)

# Summary:
- Routers are pluggable in to the main express app and other routers. 
- We can middleware or HTTP method routes to this router.
- We can modularize our routes, and this is how we can protect our routes or have specific middleware affecting this route.
---
# Related Stuff:
[[Express - Post]]
[[Express Routing]]
[[Express - Middleware]]
[[Express - NodeJs]]

#express 
#nodejs 
#webapplications 

---
# Notes:
> A `router` object is an isolated instance of middleware and routes. You can think of it as a <mark style="background: #FFB86CA6;">“mini-application,” capable only of performing middleware and routing functions</mark>. Every Express application has a built-in app router.
> A router <mark style="background: #FFB86CA6;">behaves like middleware itself</mark>, so you can use it as an argument to [app.use()](https://expressjs.com/en/4x/api.html#app.use) or as the argument to another router’s [use()](https://expressjs.com/en/4x/api.html#router.use) method.
> The top-level `express` object has a [Router()](https://expressjs.com/en/4x/api.html#express.router) method that creates a new `router` object.
> Once you’ve created a router object, you can add middleware and HTTP method routes (such as `get`, `put`, `post`, and so on) to it just like an application.

- A router is a "mini" application that can be plugged into the main express app or other routers. With this router, we can add middleware and HTTP method routes.