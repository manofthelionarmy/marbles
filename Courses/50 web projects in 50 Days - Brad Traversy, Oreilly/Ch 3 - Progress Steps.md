# Summary:
---
# Related Stuff:
[[Css - Psuedo-classes]]
[[Css - Pseudo-elements]]
[[Flexbox]]
[[Css - Root Pseudo Class]]
[[Properties applied to flex items]]
[[Css - Content Property]]
[[Css - Custom Properties]]
[[Css - var]]
#css 

---
# Notes:
- In this project, the goal was to click on prev or next button. Every time we clicked the next button, the progress bar progressed and the circles will be highlighted. 
- We modified the style with javascript.
- There were some new things introduced in css:
	- root scope via `:root` pseudo class
	- var() and custom properties
	- `::before`
	- `:focus`, `:active`, `:disabled`
	- flex, `justify-content: space-between`
- It was my first time working with disabled buttons.
- Our use of `content` in the `progress-container::before` (the pseudo-element of before) is interesting. From what I read in the documentation, it sets the content of the 'before' element, which is before the content of the actual content (the text node rendered in the dom)
- Because we set it to `''`, or an empty string, this allowed us to draw a line. Could we have done the same without use the pseduo element, but rather a real element (like a div?). If I don't set the content to `''` and set it to other possible values, the line doesn't render. The drawn line also appears if we set the content to some none empty value, ex: `'something'`. It makes sense, because if we set it to `normal` (which defaults to `none` for `::before` and `::after`). 
	- It works too if I use a div with a class selectored called `progress-empty`, and if I don't specify the `content` rule (remove it, I mean.)
```css
.progress-empty {
  /* content: '';  <- removed this*/
  background-color: var(--line-border-empty);
  position: absolute;
  top: 50%;
  left: 0;
  transform: translatey(-50%);
  height: 4px;
  width: 100%;
  z-index: -1;
}
```

```html
        <div class="progress-container">
          <div class="progress-empty"></div>
          <div class="progress"></div>
          <div class="circle active">1</div>
          <div class="circle">2</div>
          <div class="circle">3</div>
          <div class="circle">4</div>
        </div>

```

- It works because we did `position: absolute`, which means its position is relative to its closest ancestor, which is `progress-container`  in this example. So, the `progress-empty` will sit under `progress` and they'll be aligned because of `position: absolute`.
- I think this project introduced the `::before` pseudo-element and we can see it's use can solve the problem too.
- I think it's odd how we are using `max-width` and `width`. This points out my observations:
  [A Tale of Width and Max Width - Css Tricks](https://css-tricks.com/tale-width-max-width/)