[Links?](#)
[Embbed Videos?](#)
[Record Types - Dart Docs](https://dart.dev/language/records)
# Summary
- Record types allow us to have multi return values from functions.

----
# Related Stuff

----
# Notes:
- Record types work like function parameters:
	- they can be positional or named.
- We can return a record from a function, allowing multiple return values from a function.
```dart
  (String, int) myRecord;
  myRecord = ("hello", 5);
  // I can specify which element in the record by using this notation
  print("${myRecord.$1} and ${myRecord.$2}");

  ({String name, int age}) personalInfo;
  personalInfo = (name: "Armando", age: 27);
  print("${personalInfo.name} is ${personalInfo.age} years old");

  ({String name, int age}) personalInfo2 = PersonalInfoFactory("Isaiah", 27);
  print(sentence(personalInfo2.name, personalInfo2.age));
  var (name, age) = f("Olivia", 26);
  print(sentence(name, age));

({String name, int age}) PersonalInfoFactory(String name, int age) {
  return (name: name, age: age);
}

String sentence(String name, int age) {
  return "${name} is ${age} years old";
}

(String, int) f(String name, int age) {
  // just like go, expect wrap with parentheses in the return statement
  return (name, age);
}


```


## Questions:

## Follow Up:
