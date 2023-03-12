[Stack Overflow](https://stackoverflow.com/a/52699702)
# Summary:
---
# Related Stuff:
#golang 
#http 
#networks 
[[Golang - Why Decode Twice]]
[[Authentication - Building Web Applications With Go - Intermediate - Udemy]]

---
# Notes:
- We want to use MaxBytesReader so that someone doesn't send an oversized request body. I don't know what that exploits, but it may be worth following up.
- Example:
```go
func (app *application) readJSON(w http.ResponseWriter, r *http.Request, data interface{}) error {
	// 1 MB = 1048576 bits
	maxBytes := 1048576

	// make sure a user doesn't pass us a malicious oversized request body
	r.Body = http.MaxBytesReader(w, r.Body, int64(maxBytes))

	dec := json.NewDecoder(r.Body)
	err := dec.Decode(data)
	if err != nil {
		return err
	}

	// why are we decoding it again?
	// we don't want multiple entries (this is stated from the course, but I need an example where we force this error)
	err = dec.Decode(&struct{}{})
	if err != io.EOF {
		return errors.New("body must only have a single JSON value")
	}
	return nil
}

```