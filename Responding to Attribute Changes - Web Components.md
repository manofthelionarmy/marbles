[Links?](#)
[Embbed Videos?](#)
[Responding to Attribute Changes - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Components/Using_custom_elements#responding_to_attribute_changes)
# Summary

----
# Related Stuff
[[Web components]]
[[Web Components Lifecycle]]
[[Lit Web Components Playground]]
#javascript 
#webapplications 
#html 

----
# Notes:
- Web component attributes are synonymous/linked to the class properties we have in our class implementation that extends the HtmlElement.
- We can respond to the values set in the in the web components attributes set by a consumer using the custom element.

> Like built-in elements, <mark style="background: #FFB86CA6;">custom elements can use HTML attributes to configure the element's behavior</mark>. To use attributes effectively, an element has to be able to <mark style="background: #FFB86CA6;">respond to changes</mark> in an attribute's value. To do this, a custom element needs to add the following members to the class that implements the custom element:
	- A <mark style="background: #FFB86CA6;">static property</mark> named <mark style="background: #FFB86CA6;">observedAttributes</mark>. This must be an array containing the names of all attributes for which the element needs change notifications.
	 - An implementation of the <mark style="background: #FFB86CA6;">attributeChangedCallback() lifecycle callback</mark>.

> The <mark style="background: #FFB86CA6;">callback</mark> is passed <mark style="background: #FFB86CA6;">three arguments</mark>:

>  - The <mark style="background: #FFB86CA6;">name of the attribute</mark> which changed.
>  - The attribute's <mark style="background: #FFB86CA6;">old value</mark>.
>  - The attribute's <mark style="background: #FFB86CA6;">new value</mark>.

```javascript
// Create a class for the element
class MyCustomElement extends HTMLElement {
  static observedAttributes = ["size"];

  constructor() {
    super();
  }

  attributeChangedCallback(name, oldValue, newValue) {
    console.log(
      `Attribute ${name} has changed from ${oldValue} to ${newValue}.`,
    );
  }
}

customElements.define("my-custom-element", MyCustomElement);

```
- We can also use the getter to return the attributes that we observe for change. This has to  be a <mark style="background: #FFB86CA6;">static getter</mark>.
## Questions:

## Follow Up:
