# Notes
A message type is the interchangable message format in [[Protocol Buffers]]. We will decode our message into the code generate data type. 

A message can look like such:

```
syntax = "proto3";

message SearchRequest {  
	string query = 1;  
	int32 page_number = 2;  
	int32 result_per_page = 3;
}
```

Field numbers are unique numbers and assigned to each field. They are used to identify the fields in your message binary format, and should not be changed once it is in use. These fields numbers aid in forward and backward compatability, meaning no need for code changes when we use different versions of our message.

[Examples of how Fields Help With Forward/Backward Compatability](https://www.beautifulcode.co/blog/88-backward-and-forward-compatibility-protobuf-versioning-serialization)

# Related Stuff:
[[Backward and Forward Compatibility, Protobuf Versioning, Serialization]]

[[Backward and Forward Compatability]]

[[Protocol Buffers]]

[[gRPC]]

#networks 
#serialilzation 
#encoding 