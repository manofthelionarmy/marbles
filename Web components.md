[Links?](#)
[Embbed Videos?](#)
[Web components examples - github](https://github.com/mdn/web-components-examples)
[Web components Documentation - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Components)
[Lit library - github](https://github.com/lit/lit)
<iframe width="560" height="315" src="https://www.youtube.com/embed/PCWaFLy3VUo?si=L8Ll2ZqStmo1BFTo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Jy0dMy2qDMo?si=fwvjXP5UjEZIBbmA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Summary
- Web components are a browser native solution (vanilla js) to creating reusable custom elements. It is a suite of technologies that make this possible:
	- Custom elements
	- Shadow Dom
	- Html Templates
		- template
		- slots
----
# Related Stuff
[[Web Components Lifecycle]]
[[Shadow Dom]]
[[Light Dom]]
[[Html Templates Tag]]
[[Lit Web Components Playground]]

#javascript 
#webapplications 

----
# Notes:
> Web Components is a <mark style="background: #FFB86CA6;">suite of different technologies</mark> allowing you to create <mark style="background: #FFB86CA6;">reusable</mark> <mark style="background: #FFB86CA6;">custom elements</mark> — with their <mark style="background: #FFB86CA6;">functionality encapsulated</mark> away from the rest of your code — and utilize them in your web apps.

- Web components consists of three technologies
> Custom elements
>    A set of <mark style="background: #FFB86CA6;">JavaScript APIs</mark> that allow you to <mark style="background: #FFB86CA6;">define custom elements</mark> and their behavior, which can then <mark style="background: #FFB86CA6;">be used</mark> as desired in your <mark style="background: #FFB86CA6;">user interface</mark>.

> Shadow DOM
>
    A set of <mark style="background: #FFB86CA6;">JavaScript APIs</mark> for attaching an <mark style="background: #FFB86CA6;">encapsulated "shadow" DOM tree</mark> to an element — which is <mark style="background: #FFB86CA6;">rendered separately</mark> from the main document DOM — and controlling associated functionality. In this way, you can keep an element's features <mark style="background: #FFB86CA6;">private</mark>, so they can be scripted and styled <mark style="background: #FFB86CA6;">without</mark> the fear of <mark style="background: #FFB86CA6;">collision</mark> with other parts of the document.

> HTML templates
 >   The `<template>` and `<slot>` elements enable you to write <mark style="background: #FFB86CA6;">markup templates</mark> that are <mark style="background: #FFB86CA6;">not displayed</mark> in the rendered page. These can then be <mark style="background: #FFB86CA6;">reused multiple times</mark> as the <mark style="background: #FFB86CA6;">basis</mark> of a custom element's structure.

- It is now possible to create web components in all platforms  (i.e. browsers and things available in the runtime environment).
- A web component is a custom element with encapsulated behavior and properties. React, svelte kit, angular, vue, preact,bones js, etc are all solutions to implement web components with a thick layer of js. Unlike those solutions, web components are native to browsers.
- There are some concepts, or abstractions, that are needed to create web components. 
- It appears there is some boiler plate to make things work, and stuff is encapsulated via classes.
- We have to inherit from the `HTMLElement` class, and we get access to functions that are part of it's lifecycle.
- I think web components are a viable choice if we are using static web pages.  
- The web pages are more client-side now, however. We will be using the apis exposed by web platforms to insert make our custom web components available to the DOM.
- Concepts:
	- custom elements 
	- templates
		- not rendered by the dom
		- avaialable at javascript runtime 
		- we can use this to utilize the content of these elements.
	- shadow dom
		- pairing with templates, we can ensure styling is independent of each other (scoped styling versus global)
- Noice, I found a package that simplifies web components by removing the boilerplate stuff I saw by exposing an api:
	- https://github.com/lit/lit
	- i.e., it is a wrapper around web components, and it eliminates boilerplate.
- Even better, the vite tooling for generating project boilerplate supports Lit! 
## Questions:

## Follow Up:
