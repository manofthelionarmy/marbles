<iframe width="560" height="315" src="https://www.youtube.com/embed/wB9tIg209-8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
[How the single threaded non blocking IO model works in Node.js](https://stackoverflow.com/questions/14795145/how-the-single-threaded-non-blocking-io-model-works-in-node-js)

# Summary:
- When handling a request, some work being done is CPU work and other is spent on IO Work.
- CPU work is referred to active time, while I/O is referred to inactive time because we are waiting on some operation to complete. This is known as blocking I/O.
- Non-Blocking I/O doesn't wait for an I/O process to complete. Instead, the thread suspends and switches over to another task. When the task completes or is waiting for I/O process to complete, it switches back.
- This is how Node.js is able to handle Non Blocking I/O with a single thread.
---
# Related Stuff:
[[What is a Thread]]
[[Morning KeyNote - NodeJs Event Loop]]

---
# Notes:
## Follow up:
- I need to learn what a thread abstration is, and get a better picture of I/O processes.
- Watch video below another time:
<iframe width="560" height="315" src="https://www.youtube.com/embed/gMtchRodC2I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
