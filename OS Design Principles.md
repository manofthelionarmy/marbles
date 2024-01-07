[Links?](#)
[Embbed Videos?](#)
# Summary

----
# Related Stuff

----
# Notes:
- We need guiding principles of how to design an operating system.
- Separation of mechanism and policy
	- make mechanism flexible to handle a range of policies
	- e.g. LRU, LFU, random (this is cache invalidation policy)
- Optimize for common case
	- where will the os be used (the kind of machine its on, what its target env is)
	- what will the user want to execute on the machine (e.g. a database, batching process, intensive processing, etc.)
	- what are the workload requirements
- based on the common case, pick a policy that makes sense and that can be supported by the abstractions of the underlying hardware given the system.

## Questions:

## Follow Up:
