[Links?](#)
[Embbed Videos?](#)
[Bridge Pattern](https://refactoring.guru/design-patterns/bridge)

# Summary

----
# Related Stuff
[[Bridge Pattern Experiment - instance registry and ecosystem registry]] 
[[Bridge Pattern Vs Adapter Pattern]]

----
# Notes:

> This problem occurs because we’re trying to <mark style="background: #FFB86CA6;">extend</mark> the shape classes in two <mark style="background: #FFB86CA6;">independent dimensions</mark>: by form and by color. That’s a very common issue with class inheritance.
- When extending a class in independent dimensions, the class hierarchy grows. Most likely, by n-factorial (I think that's the math).
- Given we have a shape parent class, and we create sub children for colored shapes, we have red and blue. And the only shapes we have is square and circle, there for 2 shapes in total.
	- `2 * 2 = 4 total children` 
- If we add an extra shape, e.g. triangle, there are 3 total children.
	- `3 * 2 = 6 total children`
- If we were to add 2 more colors, we would have a total of 4.
	- `3 * 4 = 12 total children`
- As you can see, this scales out of control and we want to keep our class hierarchies simple and easy to keep up with.
> The Bridge pattern attempts to solve this problem by switching from inheritance to the object composition. What this means is that you <mark style="background: #FFB86CA6;">extract one of the dimensions into a separate class hierarchy</mark>, so that the original classes will <mark style="background: #FFB86CA6;">reference</mark> an object of the <mark style="background: #FFB86CA6;">new hierarchy</mark>, <mark style="background: #FFB86CA6;">instead of having all of its state and behaviors within one class</mark>.
- This means composition comes to the rescue, and we compose one class with another.
- From the gang of four book, abstractions and implementations have a different meaning within the academic context of that book in contrast to what they mean in a programming language.
- An abstraction is a high level layer that controls an entity. It delegates work to the implementation layer.
- Example: abstraction is a GUI, while the implementation is the api the GUI calls.
> You can bring order to this chaos by <mark style="background: #FFB86CA6;">extracting</mark> the code related to specific interface-platform combinations into separate classes. 

![[Pasted image 20231207200217.png]]
- As you can see here, we use composition and say the abstraction `has a` implementation.
- This is a `has a` relationship. This `has a` relationship is like a bridge.
- Though the class hierarchy doesn't grow out of control, the number of implementations does. However, we may have little abstractions, it just depends.
## Questions:
- How is this different from the Adapter Pattern?
## Follow Up:
- Review adapter pattern.
- I had this problem at work. I'm using adapter pattern for service and repository.
	- I'm not sure if this pattern is necessary.
	- The thing is that adapter pattern may seem appropriate if we have different storage or repositories (postgres, mysql, redis, mariadb, etc). The data schema won't change too much.
	- However, what if the schemas have huge differences. How do we ensure the switch is smooth as possible without changing the service and storage interface.
	- Let's check if the bridge pattern works.
