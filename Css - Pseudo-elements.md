[Pseudo-Elements MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)
# Summary
---
# Related Stuff:
[[Css - before and after pseudo-elements]]
[[Ch 3 - Progress Steps]]
#css

---
# Notes:
> A CSS **pseudo-element** is a keyword added to a selector that lets you style a specific part of the selected element(s).

> **Note:** As a rule, <mark style="background: #FFB86CA6;">double colons</mark> (`::`) should be used instead of a single colon (`:`). This <mark style="background: #FFB86CA6;">distinguishes pseudo-classes from pseudo-elements</mark>. However, since this distinction was not present in older versions of the W3C spec, most browsers support both syntaxes for the original pseudo-elements.

- An observation, parts of an html element is its text node (just the text). Therefore we can modify this part too.
- Authors specify the style and location of generated content with the `:before` and `:after` pseudo-elements. As their names indicate, the `:before` and `:after` pseudo-elements <mark style="background: #FFB86CA6;">specify the location of content</mark> before and after an element's [document tree](https://www.w3.org/TR/CSS2/conform.html#doctree) content. The ['content'](https://www.w3.org/TR/CSS2/generate.html#propdef-content) property, in conjunction with these pseudo-elements, specifies what is inserted.

- For example, the following rule inserts the string "Note: " before the content of every P element whose "class" attribute has the value "note":

```css
p.note:before { content: "Note: " }
```