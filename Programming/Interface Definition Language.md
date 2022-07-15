# Summary
- An Interface Definition language wasn't introduce in gRPC. This idea has long existed since the creation of RPC. 
- RPC is a mechanism that utilizes interface definition languages as an abstraction to define a remote method with parameters and a return type. 
- The client stub must match this signature and marshal the arguments it will pass on to the parameters of the remote method stub. When the client sub invokes itself, it invokes the remote method. The remote method on the server has it's implementation of the function, unmarshals/decodes/deserializes the data and returns it back to the client stub.
---

An interface definition language describes an **interface** in a **language agnostic** way so that software components written in different languages can communicate. For example: c++ server written in golang.

This is not tightly coupled to gRPC, actually, interface definition languages have already existed, for exmaple: RPC was a mechanism that has existed in the early days of computer networking. 

> A process on machine _A_ can call a procedure on machine _B_. When it does so, the process on _A_ is suspended and execution continues on _B_. When _B_ returns, the return value is passed to _A_ and _A_ continues execution. This mechanism is called the **Remote Procedure Call** (**RPC**).
> 	- [Paul Krzyzanowski, RPC ](https://people.cs.rutgers.edu/~pxk/417/notes/rpc.html)

This is made possible by a server **exposing an interface with method stubs that specify parameter and return types.** 

**A client stub must match the signature of the exposed method stubs** via the interface/service definition.

When the client invokes the stub, it then invokes the stub on the remote server. When this procedure completes, the process returns back the data to the client stub.

The **client stub also _marshals_/_encodes_/_serializes_ the parameters** in a network message that can be **passed on as arguments to the remote server**. The remote server then **_deserializes_/_decodes_/_unmarshals_** (given it's implementation).

JSON/XML aren't interface definition languagues, but they are data interchange formats. AKA binary formats. We use these to change our data into a format that can be sent over the network/wire.

Driving the  point home, **gRPC didn't introduce the idea of RPC. gRPC utilizes RPC by using protocol buffers as both it's message interchage-format and interface definition language**. 

Therefore, you can encode and decode messages via the protocol buffer binary format and define your service interface, which defines your remote method stubs, which messages as their parameters and messages/other data types as their return type. 



[Interface Definition Lanuage - Wikipedia](https://en.wikipedia.org/wiki/Interface_description_language)

# Related Stuff:

#networks 