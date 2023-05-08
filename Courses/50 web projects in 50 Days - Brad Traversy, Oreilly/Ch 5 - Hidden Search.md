[Links?](#)
[Embbed Videos?](#)
# Summary
----

# Related Stuff
[[Css Transitions]]
[[Css Selectors]]
#html 
#css
#javascript 

----
# Notes:
- In this project, we created a "hidden search". Practially, we click a search icon and it expends into a search bar. If we click the search icon again, an animation happens, which involves the search bar shrinking in width until it's gone and all that is left is the search icon.
- Again, we use css and javascript to achieve an animation. We made use of `transition` for our animation.
```css
.search .input {
  background-color: white;
  border: 0;
  font-size: 18px;
  padding: 15px;
  height: 50px;
  width: 50px;
  transition: width 0.3s ease; /*we create a transition with an ease effect in the even the width changes*/
}
...
.search.active .input {
  width: 200px;
}

```
- When we toggle the css class with javascript, it will have a transition with ease effect in the width shrinks or grows.
- We make the search bar and width have the same width and we make the button absolute to it's container (or enwrapping div) so that we can have the button cover and hide the search bar.
- When we toggle the `active` class for `.search`, the search input appears and we translate our search button 198px to the right while the search bar grows in width.
- More about css selectors:
```css
.search.active .input {
  width: 200px;
}

```
- Take note of `search.active`, this means we have an element that has both classes `search` and `active`.
- This means we have an element of class `search` and active that has a child element with class `input`.
## Questions:

## Follow Up:
