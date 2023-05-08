[Content Property - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/content)
# Summary:
---
# Related Stuff:
[[CSS - Replaced Elements]]
[[Css - Pseudo-elements]]
[[Ch 3 - Progress Steps]]
#css

---
# Notes:
> The **`content`** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) property <mark style="background: #FFB86CA6;">replaces</mark> an element with a generated value. Objects inserted using the `content` property are **anonymous [replaced elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Replaced_element)**.

```css
.topic-games::before {
    content: '🎮 ';
}

.topic-weather::before {
    content: '⛅ ';
}

.topic-hot::before {
    content: url('../../media/examples/fire.png');
    margin-right: 6px;
}

```