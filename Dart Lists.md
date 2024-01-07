[Links?](#)
[Embbed Videos?](#)
[Lists - Dart](https://dart.dev/guides/libraries/library-tour#collections)
[Lists declaration - stack overflow](https://stackoverflow.com/a/76427833)
[Default List Constructor Isn't Available](https://stackoverflow.com/a/63458217)
[Collection Literals](https://dart.dev/effective-dart/usage#do-use-collection-literals-when-possible)
[Collection Literals linter rule](https://dart.dev/tools/linter-rules/prefer_collection_literals)
# Summary

----
# Related Stuff
[[Dart linting]]
#dart
#flutter

----
# Notes:
- Dart has changed the way lists are initialized.
- Be wary of dynamic lists (I would stay away from this).
- The syntax for declaring a list with type is no longer supported:
```dart
List<int> myList = new List<int>();
```
- Instead, do:
```dart
var myList = <int>[];
```
- Now, we can catch errors at compile time.
- This is called a `collection literal`.
- I don't like how the book I'm using doesn't include this detail.
- I had to find some stuff on stack overflow, and some random page on the dart docs. This should be updated to include this very important detail.

## Questions:

## Follow Up:
