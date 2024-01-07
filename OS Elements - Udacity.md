[Links?](#)
[Embbed Videos?](#)
# Summary
- abstractions
- mechanisms use the abstractions
- policies dictate how to use the mechanisms to manage hardware

----
# Related Stuff

----
# Notes:
- An operating system maintains a number of high level abstractions to maintain and arbitrate underlying hardware resources, and also carries out mechanisms that utilize those high level abstractions.
- Abstractions:
	- process, thread, file, socket, memory page
- Mechanisms:
	- create, schedule, open, write, allocate
- Policies dictate how the underlying mechanisms will be used to manage the underlying hardware.
	- LRU, earliest deadline first (EDF)
- Example:
	- abstraction: memory page
	- mechanism: allocate, map to a program
	- policy: LRU

## Questions:

## Follow Up:
