[Links?](#)
[Embbed Videos?](#)
[Mixins - Dart Docs](https://dart.dev/language/mixins)
# Summary

----
# Related Stuff

----
# Notes:
- Mixins are a way of <mark style="background: #FFB86CA6;">defining code</mark> that can be <mark style="background: #FFB86CA6;">reused</mark> in <mark style="background: #FFB86CA6;">multiple class hierarchies</mark>. They are intended to provide member implementations en masse.
- In other words, classes from separate class hierarchies reusing code amongst each other without direct inheritance.
```dart
class Musician extends Performer with Musical {
  // ···
}

class Maestro extends Person with Musical, Aggressive, Demented {
  Maestro(String maestroName) {
    name = maestroName;
    canConduct = true;
  }
}
```

- In Flutter, we can use a mixin between widget class and animation class. 
## Questions:

## Follow Up:
