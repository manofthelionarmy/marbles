# Summary:
- Rust catches code that can cause unexpected behavior in the  compiler.
- Rust has many restrictions, and those same restrictions ensure concurrent programs are safe too. All tools are available to writing concurrent software.
- Rust is fast, meaning it will help us make the best use of the underlying machine's capabilities (that means best use of it's resources).
- Rust has package and version management support, as well as features that enable flexible interfaces to be built.
# Related Stuff:
# Notes:
- There are things done in programming languages, like C/C++ that can lead to unexpected behavior. Unexpected behavior is not random stuff happening, it is actually determinable what the unexpected behavior can do. These can be exploited and expose vulnerabilities in operating systems and servers. The same goes for the software written. Written software that follows the best coding guidelines can still have unexpected behaviors be exploited.
- The solution is to have the compiler catch these unexpected behaviors, which rust does.
- Therefore, Rust imposes many restrictions because of this capability to ensure you will not have unexpected behavior.
- Because of this, the same restrictions that ensure memory safety in Rust also enusre that Rust programs are free of data races. All the traditonal concurrency tools are available: mutexes, conditional variables, channels, atomics, and so on. Rust simply checks that you're using them properly.
- Normally, when we are writing software for a game, we want to push the host machine to the limits. 
- It would be more precise to say that, <mark style="background: #FFB86CA6;">if you are ready to make the investment to design your program to make the best use of the underlying machine's capabilities</mark>, Rust supports you in that effort. Therefore, we get speed.
- Rust has package and version management, making it easier for developers to collab, as well as the capability to create flexible interfaces.
- Rust is a breath of fresh air to systems programmers, because it eliminates major, well understood problems that have plagued the industry for decades.
- Systems programming is resource-constrained programming.