[Links?](#)
[Embbed Videos?](#)
[Dart class modifiers](https://dart.dev/language/class-modifiers#abstract)
# Summary

----
# Related Stuff
[[Dart Classes]]
[[Dart Class Modifiers]]
[[OOP Abstract Classes Vs Interface]]
#dart

----
# Notes:
- Abstract classes aren't classes that can be instantiated. We can only instantiate a class that extends it.
> An abstract class may have abstract members without an implementation, allowing it to be implemented by the child types that extend them

- This example illustrates the statement above.
```dart


abstract class Vehicle {
  void moveForward(int meters);
}


// Error: Cannot be constructed
Vehicle myVehicle = Vehicle();

// Can be extended
class Car extends Vehicle {
  int passengers = 4;
  // ···
}

// Can be implemented
class MockVehicle implements Vehicle {
  @override
  void moveForward(int meters) {
    // ...
  }
}

```

## Questions:

## Follow Up:
