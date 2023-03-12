[Client versus Server Side Rendering - Free Code Camp](https://www.freecodecamp.org/news/what-exactly-is-client-side-rendering-and-hows-it-different-from-server-side-rendering-bd5c786b340d/)
# Summary:
# Related Stuff:
[[Authentication - Building Web Applications With Go - Intermediate - Udemy]]
#webapplications 
#nodejs 
#golang 

# Notes:
- The client side renders the html by manipulating the dom via the browser with JS code. What is sent back is minimal html, with bundled js files, css, and assets. A client then makes requests to the api, and the client handles the responses and dynamically alters the html page via the browser with JS code in a single page application.
- The server side uses templates to dyanmically build the html via a template engine. What is sent back from the server is the "filled" in html template, which contains data from the server request, bundled js files, css, and assets. This is not a single page application, maybe more of a multipage application because we send back different html files.
- Both can be used for "dynamic websites". That is, the website can change upon server requests.
	- I'd imagine this be tricker for SSR, because we can send back JS code to alter the dom for our page. Say if a button was clicked, or some other dom event happened. We can still alter the dom.
	- By trickier, I think this will be a tough development experience if the project grows.
	- There are frameworks that can help with this to make the development experience better (Next.js, Svelte kit, etc).
- Client side rendering sounds like it can be easier to handle dom events because the client-side application can be modularized (React, Angular, Vue, Svelte, etc). The downside if the project gets bigger, this will take a while to render the app on first fetch. Maybe that's why they use CDNs (Content Delivery Networks).