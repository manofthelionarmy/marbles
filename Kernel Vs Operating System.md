[Links?](#)
[Userland or Userspace - Wikipedia](https://en.wikipedia.org/wiki/User_space_and_kernel_space)
[Embbed Videos?](#)
<iframe width="560" height="315" src="https://www.youtube.com/embed/IvGdY6luTtU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/RNeKYjWx-s4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Summary
- An operating system includes the software needed for users to interface with the kernel. That includes peripherals (mouses, keyboards, speakers, etc) and a terminal emulator and bash shell.
- The kernel allocates hardware resources to applications running in memory, aids in scheduling, etc.
- They say the kernel is the core of the OS, but a lot of definistions of the os is the same as  the kernel. 
	- If so, why do we need an OS if we can just utilize the kernel? 
- It is said the operating system can't work without the kernel, and that the kernel can't work without being in the context of the operating system. 
- I looked up the history, and GNU had "other components" (these components are in reference to software for the user interface and *userland*) and needed a kernel (software to manage the hardware resources or allocate resources to runnin programs in memory via arbitrations and policies).
- The second YouTube video is the answer to this question, and it turns out the kernel isn't responsible for user interface or userland. A distribution of an operating system will include software, firmware, desktop stuff (KDE, GNOME, XFCE, etc) and the kernel. 
- Software like a terminal emulator and the bash shell exists in userland and we can interface with our kernel (get info about hardware and abstractions (like ports, network stuff, filesystem)).
- I bet under the hood, a word processor application saves our file to the filesystem, has our written text exist in a buffer, etc, and has to interact with the kernel because we need it to interface with the filesystem, which is a abstraction that has ties to the hard disk.
![[Pasted image 20230506165933.png]]
> User space usually refers to the various programs and [libraries](https://en.wikipedia.org/wiki/Library_(computing) "Library (computing)") that the operating system uses to interact with the kernel: software that performs [input/output](https://en.wikipedia.org/wiki/Input/output "Input/output"), manipulates [file system](https://en.wikipedia.org/wiki/File_system "File system") objects, [application software](https://en.wikipedia.org/wiki/Application_software "Application software"), etc.

----
# Related Stuff

----
# Notes:

## Questions:

## Follow Up:
