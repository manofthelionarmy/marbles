[Links?](#)
[Embbed Videos?](#)
[Lit Code Labs: Define a Custom Element](https://codelabs.developers.google.com/codelabs/the-lit-path#2)
[ES Modules Specification - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
[The Javascript Modules Handbook - FreeCodeCamp](https://www.freecodecamp.org/news/javascript-es-modules-and-module-bundlers/)
[Web Components Life Cycle - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_custom_elements#custom_element_lifecycle_callbacks)
[Clone Node - DOM node api](https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode)
[Adding Functionality to Web Components- Lit Code Labs](https://codelabs.developers.google.com/codelabs/the-lit-path#5)
# Summary
- We define a custom element by associating a hyphenated tag name (i.e. this is a suggestion by google so that we can differentiate from existing tag names) with a class that extends the HTMLElement class. We do this by calling the custom elements api.
- Web components have lifecyle events we can hook into, and inversion of control.
- The first few modules of this codelab doesn't start with Lit library - it starts by teaching the technologies involved with web components: custom elements, shadow dom, html templates, ES modules.
- To use this template element, you query the template, get it's contents, and clone those nodes with templateContent.cloneNode where the true argument performs a deep clone. You then initialize the dom with the data.
- In order for web components to have attributes and they update properly in the rendered dom, you need to use getters and setters (to set the class properties/attributes on the custom element), lifecycle call back attachedAttributesCallback, and static getter for observedAttributes to return the list of attribute names.

----
# Related Stuff
[[Web components]]
[[Lit Web Components]]
[[Javascript Modules]]
[[Web Components Lifecycle]]
[[Shadow Dom]]
[[Light Dom]]
[[Html Templates Tag]]
[[Responding to Attribute Changes - Web Components]]

#javascript 
#webapplications 

----
# Notes:
### Define A Custom Element
- Though MDN documentation states that Web components consist of 3 technologies, i.e. templates, shadow dom, and custom elements, this code lab says web components says they consist of 4 parts:
	- ES modules
	- Custom Elements
	- Shadow Dom
	- HTML Elements
> You've already used the <mark style="background: #FFB86CA6;">ES modules specification</mark>, which allows you to create javascript modules with imports and exports that are loaded into the page with `<script type="module">`. 
- The codelab states that web components has one more part than the MDN docs, and that extra piece is specifying we'll use the ES Modules specification. 
	- ~~Putting some thought into this, we don't need es modules to begin with, because Web components are native to the browser. I didn't read anywhere in the MDN docs that we need to specify this. I guess this is more specific to **Lit Web Components**.~~
- After learning what ES modules are, I think it's important we need it because we are modularizing or ui components by utilizing the native Web Components. So, it's important we break out our code to encapsualte and expose any behavior.
- Actually, it's crucial we use ES modules or native web components don't work.
> A custom element is defined by <mark style="background: #FFB86CA6;">associating a class that extends HTMLElement with a hyphenated tag name.</mark> The <mark style="background: #FFB86CA6;">call to customElements.define</mark> tells the browser to associate the class RatingElement with the tagName ‘rating-element'. This means that every element in your document with the name `<rating-element>` will be associated with this class.

- Custom Elements come with a set of <mark style="background: #FFB86CA6;">lifecycle hooks</mark>. They are:
 - constructor
 - connectedCallback
 - disconnectedCallback
 - attributeChangedCallback
 - adoptedCallback
- Very neat, we can hook into the lifecycle of the web components and add behavior we wish to include during this lifecycle events.
- A use case for using a call back is doing dom manipulations. It's bad practice to do so from the constructor. It's better to do so by hooking into the lifecycle events.
- Here's all the lifecycles the lab lists out:
	- The connectedCallback is called when the custom element is attached to the DOM. This is typically where initial DOM manipulations happen.
	
	- The disconnectedCallback is called after the custom element is removed from the DOM.
	
	- The attributeChangedCallback(attrName, oldValue, newValue) is called when any of the user-specified attributes change.
	
	- The adoptedCallback is called when the custom element is adopted from another documentFragment into the main document via adoptNode such as in HTMLTemplateElement
### Shadow Dom 
- Why Shadow dom?
	- In the previous step, you'll notice that the <mark style="background: #FFB86CA6;">selectors in the style tag</mark> that you inserted <mark style="background: #FFB86CA6;">select any rating element</mark> on the page as well as any button. This may result in the <mark style="background: #FFB86CA6;">styles leaking</mark> out of the element and <mark style="background: #FFB86CA6;">selecting other nodes</mark> that you may not intend to style. Additionally, <mark style="background: #FFB86CA6;">other styles outside of this custom element may unintentionally style the nodes inside your custom element</mark>
- I.e., styling is not scoped to this custom element. It can be affected by global styling, and the styling we intended for this web component can be applied to other elements.
- We wish to encapsulate the styling specifically for the web component. 
- To solve we need to attach a `shadow root`.
- It appears there's some boiler plate: 
	- We need to create the shadow root via the shadow dom api.
	- The shadow dom api is attached to the custom element object. 
	- To make the `shadow content` inspectable (is this only limited to the Chrome Inspector, or does `open` mode do other things?) we specifiy the `mode` to be `open`.
- Because we specified the `mode` to be `open`, the `shadow content` is expandable from the browsers dev tool inspector.
![[Pasted image 20240106121033.png]]
```javascript
class RatingElement extends HTMLElement {
  constructor() {
    super();
    this.rating = 0;
    
  }
  connectedCallback() {
    const shadowRoot = this.attachShadow({mode: 'open'});
   shadowRoot.innerHTML = `
     <style>
       :host {
         display: inline-flex;
         align-items: center;
       }
       button {
         background: transparent;
         border: none;
         cursor: pointer;
       }
     </style>
     <button class="thumb_down" >
       <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M15 3H6c-.83 0-1.54.5-1.84 1.22l-3.02 7.05c-.09.23-.14.47-.14.73v2c0 1.1.9 2 2 2h6.31l-.95 4.57-.03.32c0 .41.17.79.44 1.06L9.83 23l6.59-6.59c.36-.36.58-.86.58-1.41V5c0-1.1-.9-2-2-2zm4 0v12h4V3h-4z"/></svg>
     </button>
     <span class="rating">${this.rating}</span>
     <button class="thumb_up">
       <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M1 21h4V9H1v12zm22-11c0-1.1-.9-2-2-2h-6.31l.95-4.57.03-.32c0-.41-.17-.79-.44-1.06L14.17 1 7.59 7.59C7.22 7.95 7 8.45 7 9v10c0 1.1.9 2 2 2h9c.83 0 1.54-.5 1.84-1.22l3.02-7.05c.09-.23.14-.47.14-.73v-2z"/></svg>
     </button>
   `;
   }
}
customElements.define('rating-element', RatingElement);
```
- ~~I messed around and I changed the `mode` to `close`, and the custom element didn't render, why is that?~~ 
- I was wrong. The api doesn't recognize `close` as a valid value for `mode` option. A valid value is `closed`, and the custom element still renders. The mdn docs goes in more detail about the `mode` option does.
- When adding children nodes inside the custom element, they won't render. These children nodes inside the custom element are known as the light dom.
### HTML Templates
- Why Html templates:
	- In the context of web components, we want reusability.
	- Instead of passing in a string 
> Using <mark style="background: #FFB86CA6;">innerHTML</mark> and <mark style="background: #FFB86CA6;">template literal strings</mark> with <mark style="background: #FFB86CA6;">no sanitization</mark> may cause <mark style="background: #FFB86CA6;">security issues</mark> with <mark style="background: #FFB86CA6;">script injection</mark>. Methods in the past have included using DocumentFragments, but these also come with other issues such as images loading and scripts running when the templates are defined as well as introducing obstacles for reusability. This is where the `<template>` element comes in; templates provide inert DOM, a highly performant method to clone nodes, and reusable templating.	
- Html templates is a native, highly performant, and safe solution (inert DOM, meaning cannot be manipulated via script injection) for reusing hypermedia content, or html fragments.
```html
 <template id="rating-element-template">
   <style>
     :host {
       display: inline-flex;
       align-items: center;
     }
     button {
       background: transparent;
       border: none;
       cursor: pointer;
     }
   </style>
   <button class="thumb_down" >
     <svg xmlns="http://www.w3.org/2000/svg" height="24" viewbox="0 0 24 24" width="24"><path d="M15 3H6c-.83 0-1.54.5-1.84 1.22l-3.02 7.05c-.09.23-.14.47-.14.73v2c0 1.1.9 2 2 2h6.31l-.95 4.57-.03.32c0 .41.17.79.44 1.06L9.83 23l6.59-6.59c.36-.36.58-.86.58-1.41V5c0-1.1-.9-2-2-2zm4 0v12h4V3h-4z"/></svg>
   </button>
   <span class="rating"></span>
   <button class="thumb_up">
     <svg xmlns="http://www.w3.org/2000/svg" height="24" viewbox="0 0 24 24" width="24"><path d="M1 21h4V9H1v12zm22-11c0-1.1-.9-2-2-2h-6.31l.95-4.57.03-.32c0-.41-.17-.79-.44-1.06L14.17 1 7.59 7.59C7.22 7.95 7 8.45 7 9v10c0 1.1.9 2 2 2h9c.83 0 1.54-.5 1.84-1.22l3.02-7.05c.09-.23.14-.47.14-.73v-2z"/></svg>
   </button>
 </template>

```
- Define a template, and add the elements and styling we wish to have in our web component.
- Then, in our javascript code, we need to grab the template by looking it up by it's id with the DOM api. This step will be done by hooking into the web components lifecycle.
- A very important step is to clone the templates content via the DOM node api. We will used the cloned content in our web component.
- Once we have the cloned template, we use the shadow dom api and attach it as shadow content to the shadow root.
```javascript
class RatingElement extends HTMLElement {
 constructor() {
   super();
   this.rating = 0;
 }
 connectedCallback() {
   const shadowRoot = this.attachShadow({mode: 'open'});
   const templateContent = document.getElementById('rating-element-template').content;
   const clonedContent = templateContent.cloneNode(true);
   shadowRoot.appendChild(clonedContent);

   this.shadowRoot.querySelector('.rating').innerText = this.rating;
 }
}

customElements.define('rating-element', RatingElement);

```

> To use this template element, you query the template, get it's contents, and clone those nodes with templateContent.cloneNode where the true argument performs a deep clone. You then initialize the dom with the data.
### Adding Functionality
- We would like to update the content based on some activity, like button click, or pressing a key.
> You add a <mark style="background: #FFB86CA6;">setter and getter</mark> for the rating property, and then you <mark style="background: #FFB86CA6;">update the rating</mark> element's text if it's available. This means if you were to set the rating property on the element, the view will update; give it a quick test in your Dev Tools console!

```javascript
constructor() {
  super();
  this._rating = 0;
}

set rating(value) {
  this._rating = value;
  if (!this.shadowRoot) {
    return;
  }

  const ratingEl = this.shadowRoot.querySelector('.rating');
  if (ratingEl) {
    ratingEl.innerText = this._rating;
  }
}

get rating() {
  return this._rating;
	}

```
#### Attributes Binding
- I think the terminology of web components <mark style="background: #FFB86CA6;">attributes</mark> and the actual <mark style="background: #FFB86CA6;">class</mark> implementation's <mark style="background: #FFB86CA6;">properties</mark> are used interchangeably.
- When we want to update the attributes, we need to hook into the lifecycle of the web component.
> Luckily, the Web Component lifecycle includes the <mark style="background: #FFB86CA6;">attributeChangedCallback</mark>

> In order for the attributeChangedCallback to <mark style="background: #FFB86CA6;">trigger</mark>, you must <mark style="background: #FFB86CA6;">set a static getter</mark>
> for RatingElement.<mark style="background: #FFB86CA6;">observedAttributes</mark> which <mark style="background: #FFB86CA6;">defines the attributes</mark> to be observed for changes. You then set the rating declaratively in the DOM.
#### Button Functionality
- To update values based on some dom event, we need to add event listeners. 
- As seen in the lab, we need to make use of the `bind()` function.
- See [[Why We need to bind event handlers in web components]] for why we need to do so.
> In the <mark style="background: #FFB86CA6;">constructor</mark> you <mark style="background: #FFB86CA6;">bind</mark> some click listeners to the element and keep the references around. In the <mark style="background: #FFB86CA6;">connectedCallback</mark> you <mark style="background: #FFB86CA6;">listen for click events</mark> on the buttons. In the <mark style="background: #FFB86CA6;">disconnectedCallback</mark> you <mark style="background: #FFB86CA6;">clean up</mark> these <mark style="background: #FFB86CA6;">listeners</mark>, and on the click listeners themselves, you set vote appropriately.
- So, when creating event handlers, we need to do an explicit binding, as stated here: [[Why We need to bind event handlers in web components]] 
- Then, we add the event listeners in the connectedCallback lifecycle hook.
- Then, we need to cleanup the event listeners in the disconnectedCallback lifecycle hook
- Then, we need to cleanup the event listeners in the disconnectedCallback lifecycle hook.
- Instead of explicity binding the function, we can use arrow functions. 
- Arrow functions result in the correct binding.
> The reason is that in the case of arrow functions, this is <mark style="background: #FFB86CA6;">bound lexically</mark>. This means that it <mark style="background: #FFB86CA6;">uses the context of the enclosing function</mark> — or global — scope as its this value.
- Because we will use the arrow function as the passed in value to the `addEventListener()` function in the `connectedCallBack()`, the enclosing function's scope, i.e. `connectedCallBack()` is the instantiated object is `this`.
- However, I think when we pass in cached arrow functions, I think they are garbage collected.
- I'll keep digging if this true, but explicit bindings or arrow functions (lexical binding).
> Congratulations, you now have a fully-featured Web Component; try clicking on some buttons! The issue now is that my JS file is now reaching 96 lines, my HTML file 43 lines, and the code is quite <mark style="background: #FFB86CA6;">verbose and imperative</mark> for such a simple component. This is where Google's Lit project comes in!
- As we see, the web component code grew out of control. To eliminate the boilerplate, this is where Lit comes into play!
### Lit-Html
## Questions:
- Is the `observedAttributes` arbitrary, or is it part of the HtmlElement, or web component?
	- Yes it is part of the HtmlElement or web component, see here: https://developer.mozilla.org/en-US/docs/Web/API/Web_Components/Using_custom_elements#responding_to_attribute_changes 
- Are arrow functions garbage collected?

## Follow Up:
