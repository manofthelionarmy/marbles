[Links?](#)
[Embbed Videos?](#)
[Getters and Setters - Dart Docs](https://dart.dev/language/methods#getters-and-setters)
# Summary

----
# Related Stuff
#dart 

----
# Notes:
```dart

class Rectangle {
  double left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // Define two calculated properties: right and bottom.
// odd, preface the get keyword with the return type, else it's dynamic
  double get right => left + width;

  set right(double value) => left = value - width;
  double get bottom => top + height;
  set bottom(double value) => top = value - height;
}

void main() {
  var rect = Rectangle(3, 4, 20, 15);
  assert(rect.left == 3);
  rect.right = 12;
  assert(rect.left == -8);
}


```

## Questions:

## Follow Up:
