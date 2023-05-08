[Links?](#)
[Animate on Scroll - Github](https://github.com/michalsnik/aos)
[getBoundingClientRect - MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)
[Embbed Videos?](#)
# Summary
----

# Related Stuff
[[Css Transitions]]
[[Css Selectors]]

#css 
#javascript 
#html 
#webdesgin 
#webapplications 

----
# Notes:
- We're making boxes slide in from the side. The way they slide in is alternating from left and right.
- For larger screens, we set the initial transformation of 400%.
- We used a pseudo selctor and made the even numbers of elements with `.box` slide in from the left with a transformation of -400%.
- We used `getBoundingClientRect` to get the position (relative to the height of the window) of an element.
- We calculated a "trigger bottom" to add/remove a class for elements with `.box` class. The reason is:
  we want to control at what point the boxes come in.
- If trigger the sliding boxes when the top of an element, via `getBoundingClientRect`, is at the windows inner height, `window.innerHeight`, we'll barely see the animation (it will be cut off by the viewport, animation happens off screen). 
- Hence, we want to trigger the animation at a earlier point, with respect to the inner height. That is why we are trigger the animation when we scroll to a point where we've reached 80% (4/5 ratio) of the window's inner height.
```javascript
  const triggerBottom = window.innerHeight / 5 * 4
  boxes.forEach(box => {
    const boxTop = box.getBoundingClientRect().top 
    if (boxTop < triggerBottom) {
      box.classList.add('show')
    } else {
      box.classList.remove('show')
    }

```

## Questions:

## Follow Up:
