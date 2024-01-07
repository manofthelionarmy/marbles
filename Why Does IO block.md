[Links?](#)
[Embbed Videos?](#)
[where does blocking io come from](https://stackoverflow.com/a/75027397)
# Summary

----
# Related Stuff

----
# Notes:
> The implementation of blocking I/O is that when a thread calls an I/O function, the underlying platform hosting the thread (Java VM, Linux kernel, etc.) <mark style="background: #FFB86CA6;">immediately suspends the thread</mark> so that it cannot be scheduled for execution, and also <mark style="background: #FFB86CA6;">submits the I/O request to the platform below</mark>. <mark style="background: #FFB86CA6;">When the platform receives the completion of the I/O request, it puts the result on that thread's stack and puts the thread on the scheduler's execution queue</mark>. That's all there is to the magic.

## Questions:

## Follow Up:
