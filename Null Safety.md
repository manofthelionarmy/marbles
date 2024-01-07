[Links?](#)
[Embbed Videos?](#)
[Dart Null Safety](https://dart.dev/null-safety/understanding-null-safety)
[Null Reference - Billion dollar mistake](https://www.infoq.com/presentations/Null-References-The-Billion-Dollar-Mistake-Tony-Hoare/)
# Summary

----
# Related Stuff
[[Dart Docs]]
[[Dart - Learn X in Y Minutes]]

----
# Notes:
- Null safety is the notion of ensuring we won't get a null dereference error at runtime and instead catch it a compile time.
- This prevents bug, and these bugs are dangerous because our code can be exploited. 
	- I don't know how, but it is worth watching the video.
- A null reference is this:
```go
type Example struct {}

func (e *Example) hello() {

}

func example() {
	var b *Example
	b.hello() // results in an error because this is a null reference
}
```
- This error is very transparent, but these runtime errors occur when something hasn't been properly initialized.
## Questions:

## Follow Up:
