[Links?](#)
[Embbed Videos?](#)
[Abstract Classes vs Interface](https://stackoverflow.com/questions/1913098/what-is-the-difference-between-an-interface-and-abstract-class/)
# Summary

----
# Related Stuff
[[Dart Class Constructors]]
#dart 
#oop
#golang 

----
# Notes:
> Abstract classes look a lot like interfaces, but they have something more: <mark style="background: #FFB86CA6;">You can define a behavior for them</mark>. It's more about a person saying, "these classes should look like that, and they have that in common, so fill in the blanks!".

```java
// I say all motor vehicles should look like this:
abstract class MotorVehicle
{

    int fuel;

    // They ALL have fuel, so lets implement this for everybody.
    int getFuel()
    {
         return this.fuel;
    }

    // That can be very different, force them to provide their
    // own implementation.
    abstract void run();
}

// My teammate complies and writes vehicle looking that way
class Car extends MotorVehicle
{
    void run()
    {
        print("Wrroooooooom");
    }
}
```
## Questions:

## Follow Up:
