[Express - Writting middleware for use in Express apps](https://expressjs.com/en/guide/writing-middleware.html)
# Summary:
---
# Related Stuff:
[[Middlware]]
[[Authentication - Go Web Intermediate Udemy Course]]

#express
#nodejs 
#javascript 
#webapplications 

---
# Notes:
> _Middleware_ functions are <mark style="background: #FFB86CA6;">functions</mark> that have access to the [request object](https://expressjs.com/en/4x/api.html#req) (`req`), the [response object](https://expressjs.com/en/4x/api.html#res) (`res`), and the `next` function in the application’s request-response cycle. The `next` function is a function in the Express router which, when invoked, executes the middleware succeeding the current middleware.

> Middleware functions can perform the following tasks:
>
>-   Execute any code.
>-   Make changes to the request and the response objects.
>-   End the request-response cycle.
>-   Call the next middleware in the stack.
>
> If the current middleware function does not end the request-response cycle, it must call `next()` to pass control to the next middleware function. Otherwise, the request will be left hanging.****

- It looks like the express middleware follows the pipeline design pattern. 
- In the context of express, a middlware function is defined as a function that has request and response objects and the next function as its paremeters.
- The next function exectues the succeeding middleware in the request-response cycle.
- If the middleware doesn't end the request-response cycle, the request will be left hanging. To remedy this, we must pass control to the succeeding middlware by calling `next`.
- The middlware can also do business logic or do cross cutting concerns.
## Follow up questions:
- How does routing work in express js
- How do we apply middleware to specific routes?
	- (Side thought, this will also help me understand how to protect some routes).