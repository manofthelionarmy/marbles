[Links?](#)
[Embbed Videos?](#)
[Bridge Pattern Vs Adapter Pattern - Stack Overflow](https://stackoverflow.com/a/1425325)
# Summary

----
# Related Stuff

----
# Notes:
- Adapter pattern transform data into a format that's suitable for a 3rd party application.
> The Bridge pattern is something you <mark style="background: #FFB86CA6;">implement up front</mark> - if you know you have two <mark style="background: #FFB86CA6;">orthogonal hierarchies</mark>, it provides a way to <mark style="background: #FFB86CA6;">decouple</mark> the interface and the implementation in such a way that you <mark style="background: #FFB86CA6;">don't get an insane number of classes</mark>. 
- Bridge pattern helps you decouple class hierachies that have multiple, overlapping dimensions. This makes it possible to implement and test class hierarchies independently.
- Now, we could use the adapter pattern to transform some data being handled by an implementation that uses the bridge pattern.
	- Really cool to mix and use composability with these patterns.
- Example:
```go
type Remote interface {
	ConnectAdapter(adapter DeviceAdapter)
	SetDevice(Device)
	TogglePower()
	VolumeDown()
	VolumeUp()
	ChannelDown()
	ChannelUp()
}

// Here, we create an adapter so a remote can work with other devices
type DeviceAdapter interface {
	IsEnabled() bool
	Enable()
	Disable()
	GetVolume() int
	SetVolume(volume int)
	GetChanenel() int
	SetChannel(channel int)
}

type Device interface {
	IsEnabled() bool
	Enable()
	Disable()
	GetVolume() int
	SetVolume(volume int)
	GetChanenel() int
	SetChannel(channel int)
}
```
### Mon, Dec 11, 2023:
- I think the ports and adapter pattern is cool. 
- They only give examples when the adapter is different storage systems. 
	- This is safe because the schema may not change a lot, and updates will be easy.
- However, it will be more difficult if we make adapters for 3rd party services (different apis that accomplish the same thing).
	- e.g. AWS and GCP
		- both have a different domain and schema to get the job done.
- How do we convert the core domain to either external domains/schemas via adapters?
	- what if the transformation is awkward to either domain (we can easily obtain info for one interface but are missing lots of info from the core to be used in the other domain).
		- e.g. AWS vs GCP
- Transformations would be further awkward if there is forward compatibility or backward compatibility. 
	- newer code working with older data schema
	- older code working with newer data schema.
- It would be easier to make an adapter to transform this into a sequence of bytes or some other form to be sent over the network.
	- this would avoid awkward conversions.
- However, a counter is go-gitlab. It's a cli wrapper package that hides the implementation and does the encoding under the hood; all that it requires is I pass it some data pertaining to the gitlab schema.
	- And this counter throws a wrench into what I previously thought about making an adapter to transform into a sequence of bytes. The way go-gitlab works won't work in this way.

## Questions:

## Follow Up:
