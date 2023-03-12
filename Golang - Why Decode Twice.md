[Blog Post That Says Why Decode Twice](https://mottaquikarim.github.io/dev/posts/you-might-not-be-using-json.decoder-correctly-in-golang/)
# Summary:
---
# Related Stuff:
#networks 
#golang 
[[An Architect's Guide to APIs - SOAP, REST, GraphQL, and gRPC]]]
[[Authentication - Building Web Applications With Go - Intermediate - Udemy]]

---
# Notes:
- The reason we decode twice because the request body can have a malformed/malicious request body.
- For example:
```go
package main

import (
	"encoding/json"
	"strings"
)

func main() {
    jsonData := `{
"email":"abhirockzz@gmail.com",
"username":"abhirockzz",
"blogs":[
	{"name":"devto","url":"https://dev.to/abhirockzz/"},
	{"name":"medium","url":"https://medium.com/@abhishek1987/"}
]}THIS IS INTENTIONALLY MALFORMED NOW`
    
    jsonDataReader := strings.NewReader(jsonData)
    decoder := json.NewDecoder(jsonDataReader)
    var profile map[string]interface{}
    err := decoder.Decode(&profile)
    if err != nil {
        panic(err)
    }
    // ...
}
```
- We expect this to fail, but this works and passes with flying colors. 
- Reason:
> `json.Decoder.Decode` was implemented for parsing _streaming_ JSON data, meaning it will **always** traverse the JSON string until it finds a satisfactory, closing bracket (I use the term _satisfactory_ here because it does use a stack to keep track of inner brackets).

- This explains why we did this code in the course:
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