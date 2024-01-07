[Links?](#)
[Embbed Videos?](#)
[Interfaces - Dart](https://dart.dev/language/class-modifiers#interface)
[Abstract Interfaces - Dart](https://dart.dev/language/class-modifiers#abstract-interface)
# Summary

----
# Related Stuff
[[OOP Abstract Classes Vs Interface]]
[[Combining Class Modifiers]]
[[Dart Class Modifiers]]

----
# Notes:
- A contract classes can implement without inheriting.
- Cannot instantiate an interface.
> Libraries <mark style="background: #FFB86CA6;">outside of the interface’s own defining library</mark> can <mark style="background: #FFB86CA6;">implement</mark> the interface, but <mark style="background: #FFB86CA6;">not extend it</mark>. This guarantees:
   - When one of the class’s instance methods calls another instance method on this, it will <mark style="background: #FFB86CA6;">always invoke a known implementation of the method</mark> from the same library.
>
   - <mark style="background: #FFB86CA6;">Other libraries can’t override methods</mark> that the interface class’s own methods <mark style="background: #FFB86CA6;">might later call in unexpected ways</mark>. This reduces the fragile base class problem

- Here's a sentence from the "Flutter Beginners" book I'm reading:
> Note that if you create an interface without the abstract keyword, then you can add behavior to the interface, but that would only be used if you instantiate the interface class directly; it would not be used by any classes implementing the interface.
- This is similar to golang, where you can implement an interface and add additional methods, but other implementations don't get access to them.
- It may appear this clashes with the documentation. 
	- Within the same library, we can create an implementation of the interface to abide by the contract, and additionally we can add functions to the class that aren't part of the contract.
	- Because of this, only this class implementation can get access to those functions outside of the contract and other classes don't get access to them.
- I think this is why the book mentions combining the class modifiers `abstract` and `interface` to form `abstract interface`, which enforces class implementations only abide by the contract and not extend.
	- I don't get why this is necessary. Maybe being more explicit about how you use the class, but seems pointless to add additional methods to a implementation, unless you use `reflection` like in go, then you know what type it is, and can call the function it has. 
## Questions:

## Follow Up:
