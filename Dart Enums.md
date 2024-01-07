[Links?](#)
[Embbed Videos?](#)
[Enums - Dart Docs](https://dart.dev/language/enums)
[Enhanced Enums](https://dart.dev/language/enums#declaring-enhanced-enums)
# Summary

----
# Related Stuff
[[Dart Generics]]

----
# Notes:

```dart
enum PersonType { student, employee }
```

## Enhanced Enums
- https://dart.dev/language/enums#declaring-enhanced-enums
> Dart also allows enum declarations to <mark style="background: #FFB86CA6;">declare classes with fields, methods, and const constructors</mark> which are limited to a fixed number of known constant instances.
```dart
enum Vehicle implements Comparable<Vehicle> {
  car(tires: 4, passengers: 5, carbonPerKilometer: 400),
  bus(tires: 6, passengers: 50, carbonPerKilometer: 800),
  bicycle(tires: 2, passengers: 1, carbonPerKilometer: 0);

  const Vehicle({
    required this.tires,
    required this.passengers,
    required this.carbonPerKilometer,
  });

  final int tires;
  final int passengers;
  final int carbonPerKilometer;

  int get carbonFootprint => (carbonPerKilometer / passengers).round();

  bool get isTwoWheeled => this == Vehicle.bicycle;

  @override
  int compareTo(Vehicle other) => carbonFootprint - other.carbonFootprint;
}


```
- As you can see here, comparable appears to be a generic. 

## Questions:

## Follow Up:
