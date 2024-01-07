[Links?](#)
[Embbed Videos?](#)
[Mixins - Typescript Docs](https://www.typescriptlang.org/docs/handbook/mixins.html)
[Mixins - Wikipedia](https://en.wikipedia.org/wiki/Mixin)
<iframe width="560" height="315" src="https://www.youtube.com/embed/Kn8TKLcd6d4?si=4hleCJlUprmMDTD4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
- watch whole video, great example
# Summary

----
# Related Stuff

#nodejs 
#javascript 
#typescript

----
# Notes:
- I was reading my book, Nodejs in practice, and I noticed it mentioned an approach to copy parts of a class to another object.
	- To give more context, we can inherit from the EventEmitter class.
	- An alternative approach is to copy the EventEmitter.prototype properties to an object.
- They said this approach is more "akin to a mixin, or multiple inheritance", but it seems kind of odd to do this.
- Seems easier to do in js code, but again, it looks like we can, but should we?
> In [object-oriented programming languages](https://en.wikipedia.org/wiki/Object-oriented_programming_language "Object-oriented programming language"), a **mixin** (or **mix-in**)[[1]](https://en.wikipedia.org/wiki/Mixin#cite_note-:0-1)[[2]](https://en.wikipedia.org/wiki/Mixin#cite_note-:1-2)[[3]](https://en.wikipedia.org/wiki/Mixin#cite_note-:2-3)[[4]](https://en.wikipedia.org/wiki/Mixin#cite_note-:3-4) is a [class](https://en.wikipedia.org/wiki/Class_(computer_science) "Class (computer science)") that <mark style="background: #FFB86CA6;">contains methods for use by other classes without having to be the parent class of those other classes</mark>. How those other classes gain access to the mixin's methods depends on the language. Mixins are sometimes described as being "included" rather than "inherited".
- So, in other words, we don't inherit a function, but "mixin" some functionality. So, this can bridge us a gap between two classes that have no relationship.
- So, get access to functionality without inheriting. 
- I'm not so sure of the use case. It's very complex. And not sure if it's idiomatic in typescript world.
> useful when you have an existing class and can't easily rework it to inherit directly from another class
- Therefore, you just want to bolt on some functionality to your existing class.
## Questions:

## Follow Up:
- Find some valid examples of when it's hard to inherit from something.
	- `extends` keyword helps us accomplish inheritance. When does it become complex?