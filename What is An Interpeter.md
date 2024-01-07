[Links?](#)
[Embbed Videos?](#)
[Interpreter - Wikipedia](https://en.wikipedia.org/wiki/Interpreter_(computing))
[Javascript Interpreter - Medium](https://blog.bitsrc.io/how-does-javascript-really-work-part-1-7681dd54a36d)
[V8 Runtime - Wikipedia](https://en.wikipedia.org/wiki/V8_(JavaScript_engine))
# Summary

----
# Related Stuff
[[Just In Time Compiler]]
[[How Javascript Works Behind The Scenes]]
#javascript 

----
# Notes:
> An interpreter generally uses one of the following strategies for program execution:
>1. [Parse](https://en.wikipedia.org/wiki/Parse "Parse") the [source code](https://en.wikipedia.org/wiki/Source_code "Source code") and perform its behavior directly;
>2. [Translate](https://en.wikipedia.org/wiki/Translator_(computing) "Translator (computing)") source code into some efficient [intermediate representation](https://en.wikipedia.org/wiki/Intermediate_representation "Intermediate representation") or [object code](https://en.wikipedia.org/wiki/Object_code "Object code") and immediately execute that;

> V8 first generates an [abstract syntax tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree "Abstract syntax tree") with its own parser.[[12]](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)#cite_note-12) Then, Ignition generates [bytecode](https://en.wikipedia.org/wiki/Bytecode "Bytecode") from this syntax tree using the internal V8 bytecode format.[[13]](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)#cite_note-13) TurboFan compiles this bytecode into machine code. In other words, V8 compiles [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript "ECMAScript") directly to native [machine code](https://en.wikipedia.org/wiki/Machine_code "Machine code") using [just-in-time compilation](https://en.wikipedia.org/wiki/Just-in-time_compilation "Just-in-time compilation") before executing it.[[14]](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)#cite_note-14) The compiled code is additionally optimized (and re-optimized) dynamically at runtime, based on heuristics of the code's execution profile. Optimization techniques used include [inlining](https://en.wikipedia.org/wiki/Inlining "Inlining"), [elision](https://en.wikipedia.org/wiki/Copy_elision "Copy elision") of expensive runtime properties, and [inline caching](https://en.wikipedia.org/wiki/Inline_caching "Inline caching"). The [garbage collector](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science) "Garbage collection (computer science)") is a [generational](https://en.wikipedia.org/wiki/Tracing_garbage_collection#Generational_GC_(ephemeral_GC) "Tracing garbage collection") [incremental](https://en.wikipedia.org/wiki/Tracing_garbage_collection#Stop-the-world_vs._incremental_vs._concurrent "Tracing garbage collection") collector.[[15]](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)#cite_note-15)

## Questions:

## Follow Up:
