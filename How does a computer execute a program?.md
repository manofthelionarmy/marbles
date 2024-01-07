[Links?](#)
[Embbed Videos?](#)
[Execution - Wikipedia](https://en.wikipedia.org/wiki/Execution_(computing))
[Anatomy of a program in memory ](https://stackoverflow.com/questions/14301038/how-does-a-program-runs-in-memory-and-the-way-memory-is-handled-by-operating-sys)
[Why are programs executed from memory](https://cs.stackexchange.com/questions/84206/why-are-programs-executed-in-main-memory)
[Loader - Wikipedia](https://en.wikipedia.org/wiki/Loader_(computing))
[Memory Mapped File](https://en.wikipedia.org/wiki/Memory-mapped_file)
[How does a cpu execute instructions](https://www.programmathically.com/how-does-a-cpu-execute-instructions-understanding-instruction-cycles/)
[Instruction Cycle](https://en.wikipedia.org/wiki/Instruction_cycle)
<iframe width="560" height="315" src="https://www.youtube.com/embed/Z5JC9Ve1sfI?si=bZuM303cnJcZCaSg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
[CPU Scheduling](https://en.wikipedia.org/wiki/Scheduling_(computing))
# Summary
- I got curious about how a program really executes. 
- I recall a program gets loaded into memory, but I'm hairy on the details about how the cpu executes the program.
- The OS plays a big part in this, and I need to understand how it works.
- A program is loaded into memory. It's given a range of memory addresses. It's memory mapped.
- The cpu fetches the instruction from memory, decodes, and executes it. It continues performing the instruction cycle per cycle.
- CPU scheduling ensures that we can execute multiple programs at once, hence why we can have more than one app open.

----
# Related Stuff
#computer-science

----
# Notes:
- This wikipedia describes execution:
	- [Execution](https://en.wikipedia.org/wiki/Execution_(computing))
>  Executable code, an <mark style="background: #FFB86CA6;">executable file</mark>, or an executable program, sometimes simply referred to as an executable or binary, is a <mark style="background: #FFB86CA6;">list of instructions</mark> and data to cause a computer "to <mark style="background: #FFB86CA6;">perform</mark> indicated <mark style="background: #FFB86CA6;">tasks</mark> <mark style="background: #FFB86CA6;">according to encoded instructions</mark>",[1] as opposed to a data file that must be interpreted (parsed) by a program to be meaningful. 
- Recall a executable program is the machine code generated from a compiler.
	- The machine code is something that can be read by the cpu, which abides by the cpu's instruction set architecture (ISA).
- This is the life cycle of a executable program, from beginning to end.
>Prior to execution, a program must first be <mark style="background: #FFB86CA6;">written</mark>. This is generally done in source code, which is then Prior to execution, a program must first be written. This is generally done in source code, which is then <mark style="background: #FFB86CA6;">compiled</mark> at compile time (and statically linked at link time) to produce an executable. This executable is then <mark style="background: #FFB86CA6;">invoked</mark>, most often by an <mark style="background: #FFB86CA6;">operating system</mark>, which <mark style="background: #FFB86CA6;">loads the program into memory</mark> (load time), possibly performs <mark style="background: #FFB86CA6;">dynamic linking</mark>, and then begins execution by <mark style="background: #FFB86CA6;">moving control to the entry point of the program</mark>; all these steps depend on the <mark style="background: #FFB86CA6;">Application Binary Interface</mark> of the operating system. At this point execution begins and the <mark style="background: #FFB86CA6;">program enters run time</mark>. The program then runs until it ends, either normal termination or a crash.  at compile time (and statically linked at link time) to produce an executable. 

- It's hard finding the roadmap from what point in time the cpu executes the executable program loaded memory. 
	- I would assume the cpu is agnostic of which program it's running; it's just a machine to execute low level instructions. 
	- Also, on modern computers, no programs or process executes one at a time; they are executed concurrently or in parallel, therefore they don't get sole access to the memory. That's why we have virtual memory. So then, is there some translation layer of how the program gets executed from virtual memory, or, starting from the entry point, is the CPU fed each instruction.
- Hence, why we have context switching:
> In order for programs and interrupt handlers to work without interference and <mark style="background: #FFB86CA6;">share the same hardware memory and access to the I/O system</mark>, in a <mark style="background: #FFB86CA6;">multitasking operating systems</mark> running on a digital system with a single CPU/MCU it is required to have some sort of <mark style="background: #FFB86CA6;">software and hardware facilities to keep track of an executing processes data</mark> (memory page addresses, registers etc.) and to <mark style="background: #FFB86CA6;">save and recover them back to the state they were in before they were suspended</mark>. This is achieved by a context switching.[3]: 3.3 [4] The running programs are often assigned a Process Context IDentifiers (PCID). 
- In other words, you need programs to have the access to the same hardware on the same system. 
- If there is this context switching, does it switch execution between loaded programs in memory via a address location?
- I guess in other words, I want to better understand how we get from a program being loaded into memory to run time (i.e. I want to understand the lifecycle of a program).
> Runtime, run time, or execution time is the <mark style="background: #FFB86CA6;">final phase</mark> of a computer program's life cycle, in which the <mark style="background: #FFB86CA6;">code is being executed on the computer's central processing unit (CPU) as machine code.</mark> In other words, "runtime" is the <mark style="background: #FFB86CA6;">running phase</mark> of a program.
>
>A runtime error is detected after or during the execution (running state) of a program, whereas a compile-time error is detected by the compiler before the program is ever executed. Type checking, register allocation, code generation, and code optimization are typically done at compile time, but may be done at runtime depending on the particular language and compiler. Many other runtime errors exist and are handled differently by different programming languages, such as division by zero errors, domain errors, array subscript out of bounds errors, arithmetic underflow errors, several types of underflow and overflow errors, and many other runtime errors generally considered as software bugs which may or may not be caught and handled by any particular computer language. 

- The loader is part of the operating system and it's responsibility is to load a executable program into memory.
>In the case of operating systems that support <mark style="background: #FFB86CA6;">virtual memory</mark>, the <mark style="background: #FFB86CA6;">loader may not actually copy the contents of executable files into memory</mark>, but rather may simply declare to the virtual memory subsystem that there is <mark style="background: #FFB86CA6;">a mapping between a region of memory allocated to contain the running program's code and the contents of the associated executable file</mark>. (See memory-mapped file.) The virtual memory subsystem is then made aware that pages with that region of memory need to be filled on demand if and when program execution actually hits those areas of unfilled memory. This may mean parts of a program's code are not actually copied into memory until they are actually used, and unused code may never be loaded into memory at all.  

>Fetch stage: The <mark style="background: #FFB86CA6;">next instruction is fetched from the memory address</mark> that is currently stored in the program counter and stored into the instruction register. At the end of the fetch operation, the PC points to the next instruction that will be read at the next cycle. 

- It appears a CPU fetches an instruction from memory.
- Then, does the operating system have some control (since it manages hardware) in what the cpu executes (loads from memory).
- I have to learn operating systems to understand this. If this is the case, then it makes sense if the operating system tells the cpu which memory location to look at (as the entry point or last where the program left off) because of context switching.
- I think I was confusing instruction fetch with the actual ISA fetch during the decode stage:
- instruction fetch is fetch the instruction from memory location.
- decode is decode the binary at the address location. Given the range of bits that represent the operand, the control unit then fetches from a special memory unit. This special memory unit maps operands to numerical values represented by the bits.
- I think I found the missing link:
>Another component that is involved in the CPU-scheduling function is the dispatcher, which is the <mark style="background: #FFB86CA6;">module</mark> that <mark style="background: #FFB86CA6;">gives control of the CPU to the process selected by the short-term scheduler</mark>. It receives control in <mark style="background: #FFB86CA6;">kernel mode</mark> as the result of an <mark style="background: #FFB86CA6;">interrupt or system call</mark>. The functions of a dispatcher involve the following:
>
> - <mark style="background: #FFB86CA6;">Context switches</mark>, in which the dispatcher saves the state (also known as context) of the process or thread that was previously running; the dispatcher then loads the initial or previously saved state of the new process.
> - Switching to user mode.
> - <mark style="background: #FFB86CA6;">Jumping to the proper location in the user program</mark> to restart that program indicated by its new state.
> The dispatcher should be as fast as possible since it is <mark style="background: #FFB86CA6;">invoked during every process switch</mark>. During the context switches, the processor is virtually idle for a fraction of time, thus unnecessary context switches should be avoided. The time it takes for the dispatcher to stop one process and start another is known as the dispatch latency.[7]: 155  
- Recall a process is an abstraction (data structure) maintained by the operating system. 
	- I'm pretty sure the process has information about where the program is stored in memory.
- CPU scheduling is the missing link I was looking for!
## Questions:

## Follow Up:
