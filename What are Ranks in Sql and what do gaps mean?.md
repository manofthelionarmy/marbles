[Links?](#)
[Embbed Videos?](#)
[Gaps and Rank - Sql](https://www.red-gate.com/simple-talk/databases/sql-server/t-sql-programming-sql-server/introduction-to-gaps-and-islands-analysis/)
# Summary

----
# Related Stuff

----
# Notes:
> What are gaps in SQL?

> For these examples, an island of data could be defined as a sequence of consecutive values. A gap can be defined as <mark style="background: #FFB86CA6;">a sequence of missing values</mark>. Without rounding or data modification, there are many data types for which “consecutive” has no meaning. Decimals can be ordered, but more can always be placed in between

![[Pasted image 20231127114852.png]]
> How do we solve this problem programmatically?
> <mark style="background: #FFB86CA6;">One way to identify gaps is to observe the overall row count and compare it to the expected row count</mark>, assuming no gaps existed.
![[Pasted image 20231127115303.png]]
> Note that the first column contains what should be an unbroken list of integers, assuming none are missing. The second column contains the row number, also ordered by the integer ID. The result is that <mark style="background: #FFB86CA6;">we can compare the left column to the right</mark> and in any scenario in which <mark style="background: #FFB86CA6;">the row number falls further behind our ID column</mark>, we know another <mark style="background: #FFB86CA6;">value is missing</mark>. 

> By <mark style="background: #FFB86CA6;">subtracting</mark> the row number from the integer ID, we were able to <mark style="background: #FFB86CA6;">determine the difference</mark> and knew that whenever that number increments, a new gap has been passed in the data set.

> By <mark style="background: #FFB86CA6;">comparing the next expected integer ID with the actual next integer ID</mark>, we can determine when a <mark style="background: #FFB86CA6;">gap</mark> will start and end. If the current integer is 6 and the next is 9, we immediately know that 7 and 8 are skipped and that there is an upcoming gap comprised of those two numbers.
## Questions:

## Follow Up:
