[Links?](#)
[Embbed Videos?](#)
[How Javascript Works Behind The Scenes - Freecodecamp](https://www.freecodecamp.org/news/how-javascript-works-behind-the-scenes/)
[Node Js V8 Javascript Engine](https://nodejs.org/en/learn/getting-started/the-v8-javascript-engine)
# Summary
- Javascript is an interpreted language
- This means is parsed, an abstract syntax tree is built, and the AST is used to create machine code.
	- The machine code is then executed
- Interpreters reads per statement (or line by line).
- Optimizations have been, such as JIT. 

----
# Related Stuff
[[Just In Time Compiler]]
#javascript 

----
# Notes:
> When a code snippet passes into the engine, the code is initially parsed, that is read. The code is subsequently parsed to a data structure called the abstract syntax tree (AST). The <mark style="background: #FFB86CA6;">resulting tree is then used to create machine codes</mark>.

> To fully optimize JavaScript code, <mark style="background: #FFB86CA6;">the engine first creates an unoptimized version of the machine code</mark> so it can start executing immediately. While that is ongoing, the code is being <mark style="background: #FFB86CA6;">re-optimized and recompiled in the background</mark> of the currently running program execution.
## Questions:

## Follow Up:
