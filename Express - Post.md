[Express API1- Post ](https://expressjs.com/en/5x/api.html#app.post.method)
# Summary:
---
# Related Stuff:
---
# Notes:
- Like the `use` method, which allows me to use a middleware or exeucte a callback when the request hits the specified route (url path). The difference between `post` and `use` is that post api method only exeuctes the callback if the incoming request has the matching HTTP Method POST in the request header.
	- The same idea goes for `get`, `delete`, `put`, `patch`
 - In other words, it acts like a filter (filters for HTTP methods).