[Links?](#)
[Embbed Videos?](#)
[Generics - Dart Docs](https://dart.dev/language/generics)
[Dart Generics - Dart Tutorials](https://www.darttutorial.org/dart-tutorial/dart-generics/)
# Summary

----
# Related Stuff
[[Dart Enums]]
[[Dart Abstract classes]]
#dart 

----
# Notes:
> Another reason for using generics is to <mark style="background: #FFB86CA6;">reduce code duplication</mark>. Generics let you share <mark style="background: #FFB86CA6;">a single interface and implementation between many types</mark>, while still taking advantage of static analysis. 
- A good example is creating a utilities generic, where we can perform the same set of utility functions for all of types.
- So, when you find yourself creating a bunch of abstract classes with the same set of functionality, then it's best to use generics, such as an `ObjectCache`, `StringCache`, and `NumberCache`.
	- You are still responsible for the implementation.

## Questions:

## Follow Up:
