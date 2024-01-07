[Links?](#)
[Embbed Videos?](#)
[Combining Class Modifiers](https://dart.dev/language/class-modifiers#combining-modifiers)
[Class Modifier Combinations Reference - Dart](https://dart.dev/language/modifier-reference)
# Summary
- You have fine grained control on how to modify control of how the class can be used.

----
# Related Stuff
[[Dart Classes]]
[[Dart Class Modifiers]]
[[Dart Interfaces]]
#dart




----
# Notes:
> You can combine some modifiers for layered restrictions. A class declaration can be, in order:

1. (Optional) `abstract`, describing whether the <mark style="background: #FFB86CA6;">class can contain abstract members</mark> and <mark style="background: #FFB86CA6;">prevents instantiation</mark>.
2. (Optional) One of `base`, `interface`, `final` or `sealed`, describing <mark style="background: #FFB86CA6;">restrictions</mark> on other libraries <mark style="background: #FFB86CA6;">subtyping the class</mark>.
3. (Optional) `mixin`, describing whether the declaration can be mixed in.
4. The `class` keyword itself.
- Here's a reference for all of the valid and invalid combinations:
	- https://dart.dev/language/modifier-reference
## Questions:

## Follow Up:
