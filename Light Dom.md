[Links?](#)
[Embbed Videos?](#)
[Adding Flexibility With Slots - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_templates_and_slots#adding_flexibility_with_slots)
[Terminology: Shadow Dom vs Light Dom - web.dev](https://web.dev/articles/shadowdom-v1#terminology_light_dom_vs_shadow_dom)
[Slot Element - web.dev](https://web.dev/articles/shadowdom-v1#terminology_light_dom_vs_shadow_dom)
# Summary
- We wish to have composability with web components. That means we want children nodes to be rendered inside our custom elements.
- In this abstraction, there exists 3 terms:
	- Light dom: external to shadow dom and custom elements children
	- Shadow dom: the shadow host connected to the shadow root of our custom element, and contains encapsulated js logic and scoped styling.
	- Flattened dom tree: the resulting rendered elements on the webpage, both shadow and light dom.
- `<slot>` elements acts as a placeholders, and we can render data and/or children nodes inside the web component.
	- They allow us to cross the shadow dom boundary.

----
# Related Stuff
[[Web components]]
[[Shadow Dom]]
[[Lit Web Components Playground]]
#javascript 
#webapplications 

----
# Notes:
- When utilizing the web components feature in the browser, we want composability. This means having nested children nodes, which includes but are not limited to: custom elements and html tags.
- Terminology:
	- Light dom: The markup a user of your component writes. This DOM <mark style="background: #FFB86CA6;">lives outside the component's shadow DOM</mark>. It is the element's actual <mark style="background: #FFB86CA6;">children</mark>.
	- Shadow Dom: The DOM a component author writes. Shadow DOM is <mark style="background: #FFB86CA6;">local to the component</mark> and defines its internal <mark style="background: #FFB86CA6;">structure</mark>, <mark style="background: #FFB86CA6;">scoped CSS</mark>, and <mark style="background: #FFB86CA6;">encapsulates</mark> your implementation details. It can also define how to render markup that's authored by the consumer of your component.
	- Flattened DOM tree: The result of the browser distributing the user's <mark style="background: #FFB86CA6;">light DOM</mark> into your <mark style="background: #FFB86CA6;">shadow DOM</mark>, <mark style="background: #FFB86CA6;">rendering the final product</mark>. The flattened tree is <mark style="background: #FFB86CA6;">what you ultimately see in the DevTools</mark> and what's rendered on the page.
> Shadow DOM composes different DOM trees together using the `<slot>` element. Slots are <mark style="background: #FFB86CA6;">placeholders</mark> inside your component that users can fill with their own markup. By defining one or more slots, you <mark style="background: #FFB86CA6;">invite outside markup to render in your component's shadow DOM</mark>. Essentially, you're saying "<mark style="background: #FFB86CA6;">Render the user's markup over here</mark>".

> Shadow DOM has features to control how Light DOM nodes are projected into the shadow dom via `<slot>` elements.

> Elements are allowed to <mark style="background: #FFB86CA6;">"cross" the shadow DOM boundary</mark> when a `<slot>` invites them in. These elements are called distributed nodes.

> A component can define <mark style="background: #FFB86CA6;">zero or more slots</mark> in its shadow DOM. Slots can be <mark style="background: #FFB86CA6;">empty or provide fallback content</mark>.
```html
<!-- Default slot. If there's more than one default slot, the first is used. -->
<slot></slot>

<slot>fallback content</slot> <!-- default slot with fallback content -->

<slot> <!-- default slot entire DOM tree as fallback -->
    <h2>Title</h2>
    <summary>Description text</summary>
</slot>

```

>You can also create <mark style="background: #FFB86CA6;">named slots</mark>. Named slots are specific holes in your shadow DOM that users <mark style="background: #FFB86CA6;">reference by name</mark>.
```html
<fancy-tabs>
    <button slot="title">Title</button>
    <button slot="title" selected>Title 2</button>
    <button slot="title">Title 3</button>
    <section>content panel 1</section>
    <section>content panel 2</section>
    <section>content panel 3</section>
</fancy-tabs>

<!-- Using <h2>'s and changing the ordering would also work! -->
<fancy-tabs>
    <h2 slot="title">Title</h2>
    <section>content panel 1</section>
    <h2 slot="title" selected>Title 2</h2>
    <section>content panel 2</section>
    <h2 slot="title">Title 3</h2>
    <section>content panel 3</section>
</fancy-tabs>
```
- That's the *front facing* html, here's the internals for the custom-element and where they place the slots:
```html
#shadow-root
    <div id="tabs">
    <slot id="tabsSlot" name="title"></slot> <!-- named slot -->
    </div>
    <div id="panels">
    <slot id="panelsSlot"></slot>
    </div>
```
- The front facing html uses the `slot` attribute to map to the underlying place holder `<slot>` element in the custom element.
## Questions:

## Follow Up:
