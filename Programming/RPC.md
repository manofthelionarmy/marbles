# Summary
- RPCs is a mechanism that allows software components on different machines to communicate with eachother.
- client stubs marshall data and pass as arguments to an exposed remote method's parameters. The remote method will then return data for the client to process. 
- Client stubs must match the method signature of the exposed, remote method stub.

# Notes
> A process on machine _A_ can call a procedure on machine _B_. When it does so, the process on _A_ is suspended and execution continues on _B_. When _B_ returns, the return value is passed to _A_ and _A_ continues execution. This mechanism is called the **Remote Procedure Call** (**RPC**).
> 	- [Paul Krzyzanowski, RPC ](https://people.cs.rutgers.edu/~pxk/417/notes/rpc.html)

This is made possible by a server **exposing an interface with method stubs that specify parameter and return types.** 

**A client stub must match the signature of the exposed method stubs** via the interface/service definition.

When the client invokes the stub, it then invokes the stub on the remote server. When this procedure completes, the process returns back the data to the client stub.

The **client stub also _marshals_/_encodes_/_serializes_ the parameters** in a network message that can be **passed on as arguments to the remote server**. The remote server then **_deserializes_/_decodes_/_unmarshals_** (given it's implementation).

# Related Stuff:

[[Interface Definition Language]] 

[[Encoding & Decoding]]

[[Binary Format && Binary Format Specification]]

#networks 