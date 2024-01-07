[Links?](#)
[Flutter Rendering and Layout - Docs](https://docs.flutter.dev/resources/architectural-overview#rendering-and-layout)
[Embbed Videos?](#)
<iframe width="560" height="315" src="https://www.youtube.com/embed/996ZgFRENMs?si=6gaZXxWTnoZVMw-1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<iframe width="560" height="315" src="https://www.youtube.com/embed/54yoCqkew6g?si=NPhkTi53qev9-SYW" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
# Summary

----
# Related Stuff
[[Rasterization]]
[[What is the Canvas - Flutter]]

----
# Notes:
- I'm reading a book, and they did a lazy job about describing the rendering in Flutter, and then I looked at the docs. The book was far different then what the documents displayed, and the book was published recently in 2023. 
	- Like one sentence literally said 'they move the rendering to the app'. That is not accurate. No where did they mention a rendering pipeline.
	- And they brought up the widget tree, but there's more to the architecture than just the widget tree.
- I will use the docs as the official reference for how the rendering works. 
- The videos I've attached are 
- The rendering is designed to have 3 trees:
	- widget
	- element
	- rendering object
- I lied, there's a fourth tree called the layout tree
	- I'm not sure if it's long-lived in comparison to the other 3 trees. I think it's only made before rasterization
- There's a rendering pipeline, and it's this order of operations that leads to the widgets being updated, rendering objects being updated, and widgets being drawn.
- Widgets are immutable objects. 
	- Whenever you hear `immutable`, it alludes to a new object is being instantiated.
- During a widget being updated via some animation or ui interaction, a new widget object is created an placed at the appropriate position in the widget tree. 
	- The element tree notices this, and creates a new render object and attaches to the appropriate position in the render object tree.
	- From here on out, the render object will call `paint`, which leads to the widget being drawn on the canvas.
- The reason why this design exists is to minimize the number of operations to render widgets, especially during updates.
- Actually, each widget gets its own canvas. Before rasterization, there is a phase where the drawn widgets get stitched together.
![[Pasted image 20231203111513.png]]
## Questions:

## Follow Up:
