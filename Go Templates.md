[Go Text Template](https://pkg.go.dev/text/template)
[Go Html Template](https://pkg.go.dev/html/template)
[Arguments - Go Templates](https://pkg.go.dev/text/template#hdr-Arguments)
[Pipeline - Go Html Template](https://pkg.go.dev/text/template#hdr-Pipelines)
[Actions - Go Tempaltes](https://pkg.go.dev/text/template#hdr-Actions)
[Functions - Go Templates](https://pkg.go.dev/text/template#hdr-Functions)
[Variables - Go Templates](https://pkg.go.dev/text/template#hdr-Variables)
> Go Web Programming - Ch 5, Html Templates
# Summary:
- A web template is a predesigned web template that can be used repeatedly by a template engine.
- A template engine is special piece of software that can autofill the template with data passed to it.
- Actions are commands in tell a template engine to do specfic things.
- Go's template engine allows us high reusability by nesting templates, defining templates explicitly, or creating templates with default content if one is not explicitly defined.
---
# Related Stuff:
[[Section 2 - Building a Simple Frontend and Broker Service]]
#golang 
#webapplications 
#html 

---
# Notes:
- In the context of web programming, we used tempaltes to build html documents, populate html elements with data (enrichment), and send it back to a client (the browser).
- A <mark style="background: #FFB86CA6;">web template is a predesigned HTML page</mark> that's used repeatedly by a software program, called a <mark style="background: #FFB86CA6;">tempalte engine</mark>, to generate one or more HTML pages.
- Template engines often <mark style="background: #FFB86CA6;">combine data with templates</mark> to produce the final HTML
- The <mark style="background: #FFB86CA6;">handler calls the template engine</mark>, <mark style="background: #FFB86CA6;">passing</mark> it the <mark style="background: #FFB86CA6;">template(s)</mark> to be used, usually as a list of template files and the dynamic <mark style="background: #FFB86CA6;">data</mark>. The <mark style="background: #FFB86CA6;">template engine then generates the HTML and writes it to the ResponseWriter</mark>, which adds it to the HTTP response sent back to the client
- In the Go Intermeditate Web Development Course, we used html templatese.
 - Actions, in the domain of templates, allows us (rather the tempalte engine) to take certain actions within a template. They are commands to the template engine.
- A type of action we used throughout the course was include actions, which allow us to include a template in another template. The action  looks like this: `{{ template "<name of template>" }}` or `{{ template "name of template". }}` which evalutes the data and passes it to the template.
-  Another action we used a lot is the dot (.) action. The dot (.) is an action, and it’s the most important one. The dot is the <mark style="background: #FFB86CA6;">evaluation of the data that’s passed to the template</mark>.
- Arguments can be a variable, a method (which must return either one value, or a value and an error) or a function. An argument can also be a dot (.), which is the value passed from the template engine. <mark style="background: #FFB86CA6;">An argument is a valued used in a template</mark>.
- Pipelines are arguments, functions, and methods <mark style="background: #FFB86CA6;">chained together in a sequence</mark>.
- Another action we used is `{{ define }}`. In other words, we can define multiple templates in the same template file. This allows us to have nested templates.
	- The use case of this is a `layout`. Layouts are fixed patterns in web page design that can be <mark style="background: #FFB86CA6;">reused</mark> for multiple pages.
	 - In other words, we want to increase reusability of templates.
	 - We can then use the defined template kind of like a variable within another template via the block action.
- Another action we used in the course is `{{ block "<name of defined template" }}`. The block action that allows you to define a template and use it at the same time. 
- The block action effectively <mark style="background: #FFB86CA6;">defines a template</mark>  with a provided name and also places it in the layout. If no template with a matching name is available when the overall template is executed, <mark style="background: #FFB86CA6;">the content template defined by the block will be used instead</mark>.
	- This gives us the capability to use a default, explict template.
- Most of the documentation for template actions are defined in `text/template`. Here I copy and pasted the ones we used a lot from the documentation:
```
{{template "name"}}
	The template with the specified name is executed with nil data.

{{template "name" pipeline}}
	The template with the specified name is executed with dot set
	to the value of the pipeline.

{{block "name" pipeline}} T1 {{end}}
	A block is shorthand for defining a template
		{{define "name"}} T1 {{end}}
	and then executing it in place
		{{template "name" pipeline}}
	The typical use is to define a set of root templates that are
	then customized by redefining the block templates within.
```

- We made use of variables too, for example:
```
  $variable := pipeline
```