# Summary:
---
# Related Stuff:
[[Content Delivery Network - CDN]]
[[Flexbox]]
[[Font - Awesome]]
[[Google Fonts]]
#webdesgin 
#webapplications 
#html 
#css 

---
# Notes:
- Some really notable stuff covered in this project boiler plate is some initial setup of our web page.
- That set up includes:
	- google fonts
	- flex box
	- font awesome via a cdnjs
- For fonts, we are using cdnjs (a free open source content delivery network).
- We are also using google fonts. (I don't know why we are using both awesome fonts and google fonts)
- The way we set up our boiler plate in our css file is:
```css
@import url('<google fonts url>')

* {
	box-sizing: border-box;
}

body {
	font-family: 'Roboto', sans-serif;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	height: 100vh;
	overflow: hidden;
	margin: 0;
}
```
- Some new stuff is the `box-sizing` keyword. Not sure what it does. 
	- [Box-Sizing - W3Schools](https://www.w3schools.com/csS/css3_box-sizing.asp)
- It looks like setting `box-sizing` to  `border-box` includes the padding and border in the total width and height of an element.