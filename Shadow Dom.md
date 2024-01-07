[Links?](#)
[Embbed Videos?](#)
[Shadow Dom - Lit docs](https://lit.dev/docs/components/shadow-dom/)
[Shadow Dom 101 - Web.dev](https://web.dev/articles/shadowdom-v1)
[Accessing nodes in shadow dom - lit docs](https://lit.dev/docs/components/shadow-dom/#accessing-nodes-in-the-shadow-dom)
[Shadow Dom - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM)
[Shadow Root and the mode option - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM#element.shadowroot_and_the_mode_option)
# Summary

----
# Related Stuff
[[Web components]]
[[Lit Web Components]]
#javascript 

----
# Notes:
- The shadow dom is isolated from the standard dom.
- That is why I can't query elements within the shadow dom via the dom api.

> it's important that <mark style="background: #FFB86CA6;">code running in the page should not be able to accidentally break a custom element</mark> by modifying its internal implementation.

 >Shadow DOM enables you to attach a DOM tree to an element, and <mark style="background: #FFB86CA6;">have the internals of this tree hidden</mark> from JavaScript and CSS running in the page.

 >Shadow DOM allows <mark style="background: #FFB86CA6;">hidden DOM trees to be attached to elements in the regular DOM tree</mark> — this shadow DOM tree starts with a <mark style="background: #FFB86CA6;">shadow root</mark>, underneath which you can <mark style="background: #FFB86CA6;">attach any element</mark>, in the same way as the normal DOM.
 
![[Pasted image 20240101155116.png]] 
- Shadow host: The regular <mark style="background: #FFB86CA6;">DOM node</mark> that the <mark style="background: #FFB86CA6;">shadow DOM</mark> is <mark style="background: #FFB86CA6;">attached</mark> to.
- Shadow tree: The DOM tree inside the shadow DOM.
- Shadow boundary: the place where the shadow DOM ends, and the regular DOM begins.
- Shadow root: The <mark style="background: #FFB86CA6;">root node of the shadow tree</mark>.
- Similar to the dom api, the shadom dom exposes an api to interact with the children elements within it.
> Shadow DOM <mark style="background: #FFB86CA6;">removes</mark> the <mark style="background: #FFB86CA6;">brittleness</mark> of building web apps. The brittleness comes from the global nature of HTML, CSS, and JS.
- The shadow root `mode` option specifies if the custom element is accessible from client side javascript.
	- The custom element is still available for inspection via the browser dev tools.
>we pass an argument `{ mode: "open" }` to `attachShadow()`. With mode set to "open", the <mark style="background: #FFB86CA6;">JavaScript</mark> in the page is able to <mark style="background: #FFB86CA6;">access the internals of your shadow DOM through the shadowRoot property</mark> of the <mark style="background: #FFB86CA6;">shadow host</mark>.
- In other words, it breaks encapsulation.
>The `{mode: "open"}` argument gives the page a way to <mark style="background: #FFB86CA6;">break the encapsulation</mark> of your shadow DOM. If you <mark style="background: #FFB86CA6;">don't want to give the page this ability</mark>, pass `{mode: "closed"}` instead, and then <mark style="background: #FFB86CA6;">shadowRoot returns null</mark>.
![[Pasted image 20240106122723.png]]
![[Pasted image 20240106122743.png]]
> In Shadow DOM the <mark style="background: #FFB86CA6;">:host selector</mark> refers to the node or <mark style="background: #FFB86CA6;">custom element</mark> that the <mark style="background: #FFB86CA6;">Shadow Root is attached to</mark>. 

## Questions:
- From the context of the web component, is there a way to query the elements?

## Follow Up:
