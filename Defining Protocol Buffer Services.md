# Summary:
- This is the syntax to define our RPC. When protoc runs, it will generate our client stub, and it is up to us to manually implement the exposed, remote method of our service.

> If you want to use your message types with an **RPC** (Remote Procedure Call) system, you can define an RPC service interface in a `.proto` file and the protocol buffer compiler will generate service interface code and stubs in your chosen language. So, for example, if you want to define an RPC service with a method that takes your `SearchRequest` and returns a `SearchResponse`, you can define it in your `.proto` file as follows:

```
service SearchService {  
	rpc Search(SearchRequest) returns (SearchResponse);
}
```

[Protocl Buffers Language Guide, Services](https://developers.google.com/protocol-buffers/docs/proto3#services)

# Related Stuff:
[[Protocol Buffers]]
[[Interface Definition Language]]
[[gRPC]]
[[RPC]]