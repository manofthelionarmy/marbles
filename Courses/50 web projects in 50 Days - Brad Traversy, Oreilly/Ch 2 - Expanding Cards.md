# Summary:
- We created expanding cards via advanced css background properties, flexbox, and javascript to toggle active and unactive panels to grow or shrink.
---
# Related Stuff:
[[Css Multiple Backgrounds]]
[[Css Transitions]]
[[Properties applied to flex items]]
#css 
#webapplications 
#html 
#javascript 

---
# Notes:
- We took over the boiler plate we created in ch1. We used a different font called Muli.
- We removed the `flex-direction: column` from the body. It's because we wanted the `container` to be displayed as a row item.
- These containers container `panels`, which housed the images that I got from [unspalsh.com](https://unsplash.com/)
- The main things we used in css were the css properties surrounding background, transition, flexbox, and position.
- We then modified the classlist of the panels with javascript. We added an event listener for each panel and then on the click, we removed `active` class from the other panels and added `active` class to the panel we clicked on.
- We also used a media query for devices with a smaller viewport width.
	- We also hid the 4th and 5th  panel.
- New CSS Properties:
	- background-size: specify the size of our background image
	- background-position: sets the starting position of a background image. By default, it's set at the top left corner of an element, and repeated both vertially and horizontally.
	- background-repeat: sets how background images are repeated.
	- transition: smoothly change property values over a period/duration of time.
	- flex: 
- Properties to review:
	- position
		- relative vs absolute
- Concepts to review:
	- Flexbox:
		- flex grow factor
		- flex shrink factor
		- flex basis