[CORS - MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
<iframe width="560" height="315" src="https://www.youtube.com/embed/4KHiSt0oLJ0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Summary:
---
# Related Stuff:
[[Section 2 - Building a Simple Frontend and Broker Service]]
#golang 
#nodejs 
#webapplications 
#javascript 

---
# Notes:
> **Cross-Origin Resource Sharing** ([CORS](https://developer.mozilla.org/en-US/docs/Glossary/CORS)) is an [HTTP](https://developer.mozilla.org/en-US/docs/Glossary/HTTP)-<mark style="background: #FFB86CA6;">header based mechanism</mark> that allows a server to indicate any [origins](https://developer.mozilla.org/en-US/docs/Glossary/Origin) (domain, scheme, or port) other than its own from which <mark style="background: #FFB86CA6;">a browser should permit loading resources</mark>. CORS also relies on a mechanism by which <mark style="background: #FFB86CA6;">browsers make a "preflight" request to the server hosting the cross-origin resource</mark>, in order to check that the server will <mark style="background: #FFB86CA6;">permit</mark> the actual request. In that preflight, the browser sends headers that indicate the <mark style="background: #FFB86CA6;">HTTP method and headers that will be used in the actual request.</mark>

> The CORS mechanism supports secure cross-origin requests and <mark style="background: #FFB86CA6;">data transfers between browsers and servers</mark>.
- In other words, a browser by default has the same origin policy, so if it will permit loading resources if it's coming from the same url as the web page is served on. However, if the resource needing to be loaded is not on the same origin, it will be blocked. A server needs to be configured to match the origin withing the pre-flight request from the browser. If they match, the browser will permit loading the resource.