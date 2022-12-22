# Summary:
- gRPC utilizes the concepts of RPCs to sends messages over to a service interface when the client stub is invoked. The service interface will be implemented on the server side to handle that message.
- the messages are serialized as protobufs, a binay format that is faster to serialize and deserialize than JSON.

# Related Stuff:

[gRPC Introduction](https://grpc.io/docs/what-is-grpc/introduction/)

[[Interface Definition Language]]

[[RPC]] 

[[Protocol Buffers]]

#networks
# Notes
- gRPC is a **mechanism**, rooted in RPC, that utilizes protocl buffers as its message interchange format and interface definition language. 

- A client stub, when invoked, will then encode/serialize the arguments and pass them as arguments/messages along to the exposed remote methods. This will result in the method stub being invoked, and it's implementation will unmarshall and process the message. It will then process the info, depending how the developer implemented this stub, and return some data back encoded via protocol buffer.
