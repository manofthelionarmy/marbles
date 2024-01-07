[Links?](#)
[Embbed Videos?](#)
<iframe width="560" height="315" src="https://www.youtube.com/embed/xR70UlE_xbo?si=qC7bwd7buy_qDZfV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
# Summary

----
# Related Stuff

----
# Notes:
- There are 3 known problems in concurrent systems:
	- Dirty reads
	- Non-repeatable reads
	- Phantom reads
- The isolation levels is a solution to these problems.
- The 4 isolation levels are:
	- Non-Committed Reads
	- Committed Reads
	- Repeatable Reads
	- Serializable
- Each isolation level solves the problem of the previous level:
	- committed reads prevent dirty reads
	- repeatable reads prevent non-repeatable reads and phantom reads
	- serializable allows repeatable reads and ensures that two concurrent transactions have the same result when ran in different sequential orders.
		- guarantees at least one transaction passes, the other fails.
## Questions:

## Follow Up:
