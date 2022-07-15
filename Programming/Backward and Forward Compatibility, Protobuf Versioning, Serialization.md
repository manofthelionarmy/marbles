# Summary:
- Field numbers are used to help with forward and backward compatability.
- Depending on the context: a service can choose to **ignore** it's own field if it's ahead of the client, or, it will set the field value to a specified **default** if it's behind the client's version. 
- No code changes.

# Notes
Say you have a client with Version 1 and a remote service with Version 2 of our message format. 

The service will only fill in the field it's version overlaps with, and **ignores** its own non-overlapping field.

Again, if our client has Version 2 and our service has Version 1, our client will send a message with populated fields. The service on version 1 will ignore the fields it. Since the client is expecting a response with Version 2 fields, the service will set these to **default** values.

[Source](https://www.beautifulcode.co/blog/88-backward-and-forward-compatibility-protobuf-versioning-serialization)

# Related Stuff:
[[Backward and Forward Compatability]]