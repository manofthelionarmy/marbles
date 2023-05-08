[Pseudo - Classes MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
# Summary:
- Pseudo classes allow us to apply css rules to elements, given a special state.
- That special state can be:
	- in relation to where the element is in the document tree
	- if it has a state like hovering, etc 
	- external factors, (history of navigator, its contents, like radio button was checked, etc)
 - Pseudo-classes aren't to be confused with pseudo-elements
---
# Related Stuff:
[[Css Selectors]]
[[Css - Pseudo-elements]]
[[Ch 3 - Progress Steps]]
#css

---
# Notes:
> A [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) **_pseudo-class_** is a keyword added to a selector that specifies <mark style="background: #FFB86CA6;">a special state of the selected element</mark>(s).
- In other words, we can apply css rules to elements that are in a specific state.
> A pseudo-class consists of a colon (`:`) followed by the pseudo-class name (e.g., `:hover`).

> Pseudo-classes let you apply a style to an element not only <mark style="background: #FFB86CA6;">in relation to the content of the document tree</mark>, but also <mark style="background: #FFB86CA6;">in relation to external factors</mark> like the history of the navigator ([`:visited`](https://developer.mozilla.org/en-US/docs/Web/CSS/:visited), for example), the status of its content (like [`:checked`](https://developer.mozilla.org/en-US/docs/Web/CSS/:checked) on certain form elements), or the position of the mouse (like [`:hover`](https://developer.mozilla.org/en-US/docs/Web/CSS/:hover), which lets you know if the mouse is over an element or not).

> **Note:** In contrast to pseudo-classes, [pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements) can be used to style a <mark style="background: #FFB86CA6;">specific part of an element</mark>.