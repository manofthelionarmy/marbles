[Stack overflow for converting array to slice](https://stackoverflow.com/questions/28886616/convert-array-to-slice-in-go)
[Golang blog about slices](https://go.dev/blog/slices)
[Go Slices: usage and internals](https://go.dev/blog/slices-intro#)

# Summary:
- A slice describing all the elements of the array
- Very useful to know if we need to assign an array to a slice.
# Related Stuff:
# Notes:
Also, although we haven’t used the trick yet, we can leave out the first element of a slice expression too; it defaults to zero. Thus

```go
slice[:]
```

<mark style="background: #FFB86CA6;">just means the slice itself, which is useful when slicing an array.</mark> This expression is the shortest way to say <mark style="background: #FFB86CA6;">“a slice describing all the elements of the array”</mark>:

```go
array[:]
```
