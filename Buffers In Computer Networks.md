[Buffering in Computer Networsk - geeksForGeeks](https://www.geeksforgeeks.org/buffering-in-computer-network/)
# Summary:
# Related Stuff:
# Notes
- A buffer is a temporary place holder as we move data from one place to another (from a client to a server).
> Buffers are generally used when there is a difference between the rate at which data is <mark style="background: #FFB86CA6;">received </mark>and the rate at which it can be <mark style="background: #FFB86CA6;">processed</mark>. If we remove buffers, then either we will have <mark style="background: #FFB86CA6;">data loss</mark>, or we will have <mark style="background: #FFB86CA6;">lower bandwidth utilization</mark>.
- In other words, its a temporary place holder from when we process the request. We store stuff in the buffer, the remote computers (I think network I/O) reads fromt the buffer and stitches everything together. If we don't have a buffer, we run the risk of lossing our data, or the message will be too large, resulting in latency.