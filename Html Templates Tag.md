[Links?](#)
[Embbed Videos?](#)
[Html Templates - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template)
[Deep or shallow clone node - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode#deep)
# Summary
- Not to be confused by the html templates that templating engines server side code uses to create html pages and send in the response, this is the native html `<template>` tag.

----
# Related Stuff
[[Web components]]
[[Lit Web Components]]
[[Lit Web Components Playground]]
#javascript 
#webapplications 
#html 

----
# Notes:
- HTML is one of the technologies in the native Web components feature.
>The `<template>` HTML element is a mechanism for holding HTML that is <mark style="background: #FFB86CA6;">not</mark> to be <mark style="background: #FFB86CA6;">rendered immediately</mark> when a page is loaded but may be <mark style="background: #FFB86CA6;">instantiated subsequently during runtime using JavaScript</mark>.

> ... a <mark style="background: #FFB86CA6;">content fragment</mark> that is being <mark style="background: #FFB86CA6;">stored</mark> for subsequent use in the document. While the <mark style="background: #FFB86CA6;">parser</mark> does <mark style="background: #FFB86CA6;">process</mark> the <mark style="background: #FFB86CA6;">contents</mark> of the `<template>` element while loading the page, it does so only to <mark style="background: #FFB86CA6;">ensure</mark> that those <mark style="background: #FFB86CA6;">contents are valid</mark>; the element's contents are <mark style="background: #FFB86CA6;">not rendered</mark>, however.
- Normally, we want to clone the content of the template. We use the DOM node api.
- The `cloneNode` function allows us to clone the content of the template. It has a parameter called deep, which is a boolean.
> <mark style="background: #FFB86CA6;">If true, then the node and its whole subtree, including text that may be in child Text nodes, is also copied.
</mark>

> If false, only the node will be cloned. The subtree, including any text that the node contains, is not cloned.

- It appears common to do a deep clone of the template because our web component may even have children, given the light dom.
## Questions:

## Follow Up:
