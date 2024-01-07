[Links?](#)
[Embbed Videos?](#)
# Summary
- operating systems abstract and arbitrate underlying hardware system
- hide hardware complexity
- resource management
- provided isolation and protection

----
# Related Stuff
[[Operating System Examples]]
[[OS Elements - Udacity]]
[[OS Design Principles]]
[[OS Protection Boundary]]
#os


----
# Notes:
- An operating system <mark style="background: #FFB86CA6;">abstracts</mark> and <mark style="background: #FFB86CA6;">arbitrates</mark> the underlying hardware system.
- There is not one definition of an operating system. Instead, we define an operating system by its functionality (i.e. what tasks it does)
- An operating system:
	- hides hardware complexity
		- i.e: applications don't need to know the underlying, low-level details of how hardware devices work.
		- an operating system is the layer that sits between applications and hardware complexity
		- operating system exposes higher level abstractions that applications or developers can use to interact with lower level hardware.
	- does resource management
		- operating systems creates resources, or data structures (i.e. high level abstractions) to help manage hardware.
		- example: operating system allocates memory for an application and does cpu scheduling so the application can be executed by the cpu. The resource it creates is the process, which is a highlevel abstraction of the application loaded into memory and being executed by the cpu.
		- resource allocations and resource management tasks 
	- provides isolation and protection
		- ensures each application or program run independent of one another and don't have access to each other's memory.
- An operating system is a layer of systems software that:
	- directly has <mark style="background: #FFB86CA6;">privileged access to the underlying hardware</mark>.
	- hides the <mark style="background: #FFB86CA6;">hardware complexity</mark>
	- <mark style="background: #FFB86CA6;">manages</mark> hardware on behalf of one or more applications according to some predefined policies
	- in addition, it ensures that applications are <mark style="background: #FFB86CA6;">isolated and protected</mark> from one another.
## Questions:

## Follow Up:
