[Stack Overflow - Why use HTTP Strip Prefix](https://stackoverflow.com/a/27946132)
# Summary:
In incoming request is asking for a request, but the incoming requests url doesn't match the path where the file lives in the filesystem relative from where the process (host server) is running.

# Related Stuff:
#http
#golang

# Notes:
- Example, say we have a resource available at `/tmpfiles/example.txt`. We serve the file on our server via its own filesystem, and it is found at `/tmp/examples.txt`. 
- The incoming request has this snippet as part of its URL: `/tmpfiles/exmaple.txt`. Because we have the resource on our filesystem in the `tmp` directory, we have to strip the `/tmpfiles/` prefix from the URL and replace it with `/tmp` (the directory where our resource lives). The directory has to be relative to where the process (host server)  is running.
```go
// To serve a directory on disk (/tmp) under an alternate URL
// path (/tmpfiles/), use StripPrefix to modify the request
// URL's path before the FileServer sees it:
http.Handle("/tmpfiles/",
        http.StripPrefix("/tmpfiles/", http.FileServer(http.Dir("/tmp"))))
```
