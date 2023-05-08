# Summary:
---
# Related Stuff
#html 
#css
#javascript 

---
# Notes:
- There was a lot of styling in this one.
- What we were doing was rotating an entire blog page by -20 degrees. There are other elements of the blog page that we were using the `transition` and `transform` rules. We were rotating the button. This button had two icons, and we were also applying those `transform` and `transition` propreties to them too. Lastly, we had a nav element styled to have the `li`'s staggered and to have a smooth transition into those staggered positions as we rotated the blog page.
- The javascript was simple. All we were doing was adding and removing the `show-nav` class from the class list.
- Some stuff to look into:
	- transform-origin
	- transform
	- transition
	- advanced selectors (`+` selector)
	- overflow-x
- There are some other neat tricks I want to process and I'll show their code:
```css
.circle {
  background-color: #ff7979;
  height: 200px;
  width: 200px;
  border-radius: 50%;
  position: relative; 
  /* why did we add a transition too?*/
  /* because when we toggle of show nav, we want this to ease back in*/
  transition: transform 0.5s linear;
}

```
- So, we added a transition. When we rotate it to show and hide the close button, we want to do a smooth transition.
```css
/*why did we apply this rule via this selection?*/
.container.show-nav .circle {
  /* why did we do this?*/
  /* to show the other icon*/
  transform: rotate(-70deg);
}

```
- This is a really neat trick. We are toggling the `show-nav` class and only want to apply this transform only when we've added `show-nav` to the class list. This allows us to toggle on and off styling via adding/removing from the class list in javascript.
```css
.circle button#close {
  top: 60%;
  transform: rotate(90deg);
  transform-origin: top left;
}
```
- In the styling above, we wanted to hide the close button. So we rotated it by 90% clockwise. We also set the transform-origin to the top left.
- There's a lot of styling like this actually. All of this styling was done to make the rotation of the page and the elements possible. This moreso illustrates what is possible and how to achieve smooth ui experiences.
- It sounds more enticing to take that css animation course.