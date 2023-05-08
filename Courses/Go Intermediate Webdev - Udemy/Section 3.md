[Links?](#)
[Embbed Videos?](#)
# Summary
- We used flags to configure our web application.
- Our webapplication is an api server that sends back html, css, and javascript to the browser.
- We fill in the html with data via templates and go supports templating out of the box.
- We used bootstrap and stripes css styling via an open source CDN.
- The architecture of design of this app is an web api server that returns the html, css, and js needed to render and manipulate our web application. The web application then makes api requests to our backend server via javascript and the Fetch API. We handled the responses from the backend server and manipulate the dom.
- We made our own lightweight template cache to cache built templates. We would then use the templates to render html pages with our data.
- It maybe worth it to note that template engines aren't specific to Go. There are a bunch of template engines that exist for different ecosystems (nodejs, express, etc). Php is an example, even now SPA applications are getting to big, and application development is moving towards rendering applications on a server via templating mechanism.
----
# Related Stuff
[[Go Templates]]
[[Content Delivery Network - CDN]]
[[Golang Flags Package]]
[[Golang Project Layout]]
[[Go Compiler Directives]]
[[What is a Layout in Web Design]]
[[Using the Fetch API - MDN]]


#golang 
#html 
#css
#javascript  

----
# Notes:
### Setting up Web Application
- We set up our frontend web application to accept flags. Interesting pattern, we are executing the application kind of like a cli and configuring it via flags. I've seen this pattern before in k8s, etcd, etc.
- We parsed the flags into a struct's properties by reference, as such:
```go
	var cfg config

	flag.IntVar(&cfg.port, "port", 4000, "Server port to listen on")
	flag.StringVar(&cfg.env, "env", "development", "Application environment {development|production}")
	flag.StringVar(&cfg.api, "api", "http://localhost:4001", "URL to api")

	flag.Parse()

```
### Setting up Routes and Rendering Application
- We set up an api server. How it will work is that we will route requests and return html, css, and js. How web servers work is that they send you back documents. When you are navigating to a website, the server returns you html, css, and js files that the browser loads. After it loads, it uses the files to render your website or webapplication.
- These documents are resources. When you hit a websites domain, you are routed to the server (via TCP/IP). Further routing needs to happen at the application layer to get you to the resource. Its up to use how we route, or we can use a routing packge. 
- Howevever, we need to populate/fill in our html pages with data we get back from the server. A template engine solves this for us. Golang has out of the box support for html templates in its standard library. It provides a template engine and an api to render documents and send it back in the response.
- In golang, we are using http handlers to handle requests hitting a specific route. Chi handles the routing for us, all we have to do is write the handler of the request and send a response back from within those handlers.
- The web api server basically handles request from a client (browser) and sends back html, css, and js for the browser to load and render.
- An important technique Trevor introduced is **template caching.**
- We also made templates and partial templates. 
- We used an embedded filesystem too for our templates. The reason is because at runtime, our application doesn't have access to the files (unless if we made them avaialble on the server we running the applicaiton). Though we didn't, it was cool to use learn about this feature that go provides; another tool added to the toolbelt.
	- For our html and css, we used the styling from bootstrap and stripejs from the open sourced cdn https://cdnjs.com/.
## Questions:
- What is template caching?
	- In this project, we were using partials and templates. We have the main template, which would house nested templates, except that we made it flexible and highly reusable to load in whatever partial template we wanted.
	- We then need to created a template object based on these files we were loading from the filesystem.
- Why do we need template caching? 
	 - It takes time to access the embedded filesystem and to create templates. We instead wanted to cache the built templates.
	 - This would save some time by caching the built templates. We would still use these cached built templates and fill them in with data we processed on the backend.
- Does golang offer template caching or do we have to implement it?
	- It doesn't. I'm not sure if there are packages that do this to us, but it seems like we can make our own lightweight internal package that can handle this for us.
- What are templates and what are partrial templates? How is this achieved in go?
	- Refer to [[Go Templates]] for in depth of how to use templates. To summarize what we did in the video using templates and made it possible to load in partial templates: partial tempaltes are like nested templates. Though we made this an option, we never took it. Instead. We used 'pages' to point to or reference the base layout. We defined nested templates that would be loaded into the base layout template that we were refering to.
 ```html
{{template "base" . }}

{{define "title"}}
    Payment Succeeded!
{{end}}

{{define "content"}}
    <h2 class="mt-5">Payment Succeeded</h2>
    <hr>
    <p>Payment Intent: {{index .Data "pi"}}</p>
    <p>Cardholder: {{index .Data "cardholder"}}</p>
    <p>Email: {{index .Data "email"}}</p>
    <p>Payment Method: {{index .Data "pm"}}</p>
    <p>Payment Amount: {{index .Data "pa"}}</p>
    <p>Currency: {{index .Data "pc"}}</p>
{{end}}

```

- An example of us using an http handler to render the template for a page.
```go
func (app *application) VirtualTerminal(w http.ResponseWriter, r *http.Request) {
	stringMap := make(map[string]string)
	stringMap["publishable_key"] = app.config.stripe.key

	if err := app.renderTemplate(w, r, "terminal", &templateData{
		StringMap: stringMap,
	}); err != nil {
		app.errorLog.Println(err)
	}
}

```
## Follow Up:
- Though we never took the option, how would we use the partial pages functionality in `renderTemplate` ?