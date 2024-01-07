[Links?](#)
[Embbed Videos?](#)
# Summary
- user mode
- kernel mode
- user mode doesn't have access to hardeware, kernel mode does
- operating system exposes api called system calls to user mode
- signals are provided by operating system and applications in user mode can subscribe or listen to them.
----
# Related Stuff

----
# Notes:
- There needs to be granted access to hardware.
- There's two modes of privileged access:
	- user-level (unprivileged)
	- kernel-level (privileged)
- operating system is software that has kernel-level privilege.
	- it has direct access to hardware
- applications are programs or software that has user-level access
	- means they don't have direct access to underlying hardwre.
- user - kernel mode switch is supported by hardware
	- i.e. there is something that specifies or distinguishes if we are in kernel mode (operating system is running)  or user mode (application is running)
	- if an application is in user mode and is trying to get access to hardware, a trap instruction is executed.
		- application process is stopped
			- control is switched back to the operating system 
			- operating system handles trap
- system call interface allows applications to interface with kernel
	- api layer that lets us ask the kernel to do something for us. 
	- open file, send socket, mmap, etc
- ^ Analogy:
	- a bank
		- actors involved: customer, bank teller
		- a customer doesn't have privileged access to do the underlying process to carry out transaction.
		- a bank teller has privileged access to facilitate bank processes.
		- a customer can't walk towards the same side of the glass the bank teller is on and implements the bank processes
			- safety measures in place
				- sound the alarm
			- the customer can mess something up because it doesn't know the underlying details of the bank process.
		- the customer would have to interact with the bank teller so they can perform the necessary underlying details:
			- "Hi, I would like to make a withdrawl. I also want to open an account and make it certificate of deposit."
- operating system also provides `signals`, which is a mechanism to send notifications (message payloads with data) and an application in user mode can subscribe to them.
## Questions:

## Follow Up:
