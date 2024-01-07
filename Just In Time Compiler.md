[Links?](#)
[Embbed Videos?](#)
[Just in time compilation](https://en.wikipedia.org/wiki/Just-in-time_compilation)
# Summary

----
# Related Stuff

----
# Notes:
> In [computing](https://en.wikipedia.org/wiki/Computing "Computing"), **just-in-time** (**JIT**) **compilation** (also **dynamic translation** or **run-time compilations**)[[1]](https://en.wikipedia.org/wiki/Just-in-time_compilation#cite_note-Michigan-1) is [compilation](https://en.wikipedia.org/wiki/Compiler "Compiler") (of [computer code](https://en.wikipedia.org/wiki/Computer_code "Computer code")) during execution of a program (at [run time](https://en.wikipedia.org/wiki/Run_time_(program_lifecycle_phase) "Run time (program lifecycle phase)")) rather than before execution.[](https://en.wikipedia.org/wiki/Just-in-time_compilation#cite_note-FOOTNOTEAycock2003-2)

> JIT compilation is a combination of the two traditional approaches to translation to machine code—ahead-of-time compilation (AOT), and [interpretation](https://en.wikipedia.org/wiki/Interpreter_(computing) "Interpreter (computing)")—and combines some advantages and drawbacks of both.[[](https://en.wikipedia.org/wiki/Just-in-time_compilation#cite_note-FOOTNOTEAycock2003-2)

- In a bytecode-compiled system, source code is <mark style="background: #FFB86CA6;">translated</mark> to an intermediate representation known as <mark style="background: #FFB86CA6;">bytecode</mark>. Bytecode is <mark style="background: #FFB86CA6;">not the machine code</mark> for any particular computer, and may be portable among computer architectures. <mark style="background: #FFB86CA6;">The bytecode may then be interpreted by, or run on a virtual machine.</mark> The <mark style="background: #FFB86CA6;">JIT compiler reads the bytecodes</mark> in many sections (or in full, rarely) and <mark style="background: #FFB86CA6;">compiles them dynamically into machine code</mark> so the program can run faster.
- It appears that we interpret the language into bytecode, then the bytecode is compiled dynamically into machine code by the JIT compiler.
	- Similar to java being translated into bytecode and executed by the JVM. (Or something like that, I can't remember the architecture of Java).
 > By contrast, a traditional _interpreted virtual machine_ will simply interpret the bytecode, generally with much lower performance. Some _interpreter_s even interpret source code, without the step of first compiling to bytecode, with even worse performance. _Statically-compiled code_ or _native code_ is compiled prior to deployment. A _dynamic compilation environment_ is one in which the compiler can be used during execution.
## Questions:
- Do just in time compilers use an interpreter?
	- yes
- Do just in time compilers interprets a piece of code then compiles? 
	- kind of
## Follow Up:
