[Properties applied to flex items](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox#properties_applied_to_flex_items)
[Controlling ratios of flex items along the main axis](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Controlling_Ratios_of_Flex_Items_Along_the_Main_Ax)

# Summary:
- The flex property controls our flex items, and it has to do more with the concept of available space.
- Flex box controls how the flex items (the children of an element with `display: flex`) are distributed amongst the available space.
- Flex-basis, flex-grow, and flex-shrink gives us more fine graned control on how these flex items can grow/fill in the space and also how the space is distributed amongst them.

---
# Related Stuff:
[[Ch 2 - Expanding Cards]]
[[Flexbox]]
#webapplications 
#webdesgin 
#css 
#html 

---
# Notes
> To have more control over flex items we can target them directly.	
- We do this by way of 3 properties:
	- flex-grow
	- flex-shrink
	- flex-basis
 > What we are doing when we change the value of these flex properties is to <mark style="background: #FFB86CA6;">change the way that available space is distributed amongst our items</mark>.

> If we instead would like the items to <mark style="background: #FFB86CA6;">grow</mark> and <mark style="background: #FFB86CA6;">fill</mark> the space, then we need to have a method of <mark style="background: #FFB86CA6;">distributing the leftover space</mark> between the items.

- This is what the `flex` properties that we apply to the items themselves, will do.
- The `flex-basis` is what defines the size of that item in terms of the space it leaves as available space.
	- pretty much, the size of the item will be set based on how much available size is leftover. 
- With the `flex-grow` property set to a positive integer, flex items can grow along the main axis from their `flex-basis`
- Where the `flex-grow` property deals with adding space in the main axis, the `flex-shrink` property controls how it is taken away. If we do not have enough space in the container to lay out our items, and `flex-shrink` is set to a positive integer, then the item can become smaller than the `flex-basis`.

> **Note:** These values for `flex-grow` and `flex-shrink` are proportions. Typically if we had all of our items set to `flex: 1 1 200px` and then wanted one item to grow at twice the rate, we would set that item to `flex: 2 1 200px`. However you could also use `flex: 10 1 200px` and `flex: 20 1 200px` if you wanted.