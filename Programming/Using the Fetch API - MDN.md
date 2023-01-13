[Using the Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

# Summary:
- The reason for the second then statement in the example is that the response object is returned as a Promise. When it is resolved, it is not only the response body, but the entire http response (response headers, response body, other data, etc). We then need to get the json response body via `.json()` which returns a second promise, with the resolved result being the parsed JSON. That is why we have a second `.then()` invocation.
---
# Related Stuff:
#javascript 
#nodejs 
#webapplications 

---
# Notes:

A basic fetch request is really simple to set up. Have a look at the following code:

```javascript
fetch('http://example.com/movies.json')
  .then((response) => response.json())
  .then((data) => console.log(data));
```

Here we are fetching a JSON file across the network and printing it to the console. The simplest use of `fetch()` takes one argument — the path to the resource you want to fetch — and does not directly return the JSON response body but instead returns a promise that resolves with a [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) object.

The [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) object, in turn, <mark style="background: #FFB86CA6;">does not directly contain the actual JSON response body but is instead a representation of the entire HTTP response</mark>. So, to <mark style="background: #FFB86CA6;">extract the JSON body content</mark> from the [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) object, we use the [`json()`](https://developer.mozilla.org/en-US/docs/Web/API/Response/json "json()") method, which <mark style="background: #FFB86CA6;">returns a second promise</mark> that <mark style="background: #FFB86CA6;">resolves with the result of parsing the response body text as JSON</mark>.