[Gob Encoding - Docs](https://pkg.go.dev/encoding/gob#Register)

<iframe width="560" height="315" src="https://www.youtube.com/embed/SE13kcjJ_X0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Summary:
- Gob encoding is a binary specificaton format that differs from json and protobufs.
- Under the hood, scs package uses gob encoding.
- Therefore, we need to tell the go compiler about the type we will store in a session. The value we are storing in the session is a non-primative, and that is why we have to take a step.
# Related Stuff:
[[Golang SCS Session Management Package]]
#golang 

# Notes:
> When you want to put a non-primitive into the session (a primitive being something like an int or a string), you have to tell the compiler that you are going to do so. This is simply because Go has strict typing, and the compiler needs to know what types you are going to be  putting in the session.
> - Trevor Sawler, Building Web Applications With Go - Intermediate Level, Udemy

> The alexedwards/scs library explains this in the Readme under _Working with Session Data_.  
 "Behind the scenes SCS uses gob encoding to store session data, so if you want to store custom types in the session data they must be **registered** with the encoding/gob package first. Struct fields of custom types must also be exported so that they are visible to the encoding/gob package. Please see here for a working example."
> - Ivor Scott, Q&A from Building Web Applications With Go - Intermediate Level, Udemy

```go
...
func main() {
	gob.Register(map[string]interface{}{})
... 
```