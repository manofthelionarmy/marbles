[Links?](#)
[Embbed Videos?](#)
[Inversion Control - Martin Fowler](https://martinfowler.com/bliki/InversionOfControl.html)
# Summary

----
# Related Stuff

----
# Notes:
> The control is inverted - <mark style="background: #FFB86CA6;">it calls me</mark> rather me calling the framework. This phenomenon is Inversion of Control (also known as the Hollywood Principle - "Don't call us, we'll call you").
- In procedural code, we have control of what to call, instantiate, calculate, etc.
- Inversion control instead calls our code instead of us calling it.

> <mark style="background: #FFB86CA6;">Inversion of Control is a key part of what makes a framework different to a library</mark>. A library is essentially a set of functions that you can call, these days usually organized into classes. Each call does some work and returns control to the client.

> A framework <mark style="background: #FFB86CA6;">embodies some abstract design</mark>, with more <mark style="background: #FFB86CA6;">behavior</mark> <mark style="background: #FFB86CA6;">built in</mark>. In order to use it you need to <mark style="background: #FFB86CA6;">insert your behavior into various places in the framework</mark> either by subclassing or by plugging in your own classes. The framework's code then calls your code at these points.

- The main difference between a library and framework is:
	- we hand over control to the library. It does some stuff, and it returns control back to the client (i.e. the program consuming and using the library).
	- In a framework, we give it our source code, it does somethings and decides when to call our code whenever it deems necessary.
- I guess I can say this:
	- because some code follows inversion of control pattern doesn't mean its a framework. 
	- A framework uses inversion of control pattern, along with other abstract design choices and with more behavior built in. 
	- A framework may include more stuff than the abstractions and built in features, I'm assuming it would include a test suite to help you easily test and make assertions that when your code is called, it behaves accordingly. I've seen frameworks also include project scaffolding.
## Questions:

## Follow Up:
