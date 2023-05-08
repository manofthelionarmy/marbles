[Publishing Modules](https://go.dev/doc/modules/publishing)
[Go Proxy](https://proxy.golang.org/)
[Module Privacy - Gives Insight about how the proxy and no proxy stuff works](https://go.dev/ref/mod#private-module-privacy)
[Go Modules reference](https://go.dev/ref/mod)
[Golang Environment Variables ](https://go.dev/ref/mod#environment-variables)
[Embbed Videos?](#)
# Summary
----

# Related Stuff

----
# Notes:
- This article shows how we can publish and pull in go modules if they don't follow:
```go
module github.com/yada/yada
```
- Instead, we can do something like:
```go
module example.com/yada/yada
```
- These are the final steps from the blog. What they highlight is we can still host our package on github, and to avoid that our package won't resolve, we follow the steps.
-   Push the new tag to the origin repository.
    
    ```
    $ git push origin v0.1.0
    ```
    
-   Make the module available by running the [`go list` command](https://go.dev/cmd/go/#hdr-List_packages_or_modules) to prompt Go to update its index of modules with information about the module you’re publishing.
    
    Precede the command with a statement to set the `GOPROXY` environment variable to a Go proxy. This will ensure that your request reaches the proxy.
    
    ```
    $ GOPROXY=proxy.golang.org go list -m example.com/mymodule@v0.1.0
    ```
- Developers will then be able to run `go get` with our module.
- Two keywords may be used in place of proxy URLs:
	-   `off`: disallows downloading modules from any source.
	-   `direct`: <mark style="background: #FFB86CA6;">download directly from version control repositories instead of using a module proxy.</mark>
- `GOPROXY` defaults to `https://proxy.golang.org,direct`. Under that configuration, the `go` command <mark style="background: #FFB86CA6;">first contacts the Go module mirror run by Google, then falls back to a direct connection if the mirror does not have the module.</mark> See [https://proxy.golang.org/privacy](https://proxy.golang.org/privacy) for the mirror's privacy policy. The `GOPRIVATE` and `GONOPROXY` environment variables may be set to prevent specific modules from being downloaded using proxies. See [Privacy](https://go.dev/ref/mod#private-module-privacy) for information on private proxy configuration.
- See [Module proxies](https://go.dev/ref/mod#module-proxy) and [Resolving a package to a module](https://go.dev/ref/mod#resolve-pkg-mod) for more information on how proxies are used.
- When the `go` command downloads a module in `direct` mode, it starts by locating the repository that contains the module.

- If the module path has a VCS qualifier (one of `.bzr`, `.fossil`, `.git`, `.hg`, `.svn`) at the end of a path component, the `go` command will use everything up to that path qualifier as the repository URL. For example, for the module `example.com/foo.git/bar`, the `go` command downloads the repository at `example.com/foo.git` using git, expecting to find the module in the `bar` subdirectory. The `go` command will guess the protocol to use based on the protocols supported by the version control tool.

- If the module path does not have a qualifier, the `go` command sends an HTTP `GET` request to a URL derived from the module path with a `?go-get=1` query string. For example, for the module `golang.org/x/mod`, the `go` command may send the following requests:

```
https://golang.org/x/mod?go-get=1 (preferred)
http://golang.org/x/mod?go-get=1  (fallback, only with GOINSECURE)
```
  
## Questions:
- If we need to prompt Go to update its index of modules, we need to use GOPROXY, as shown above. If that's the case, then what's the point of GONOPROXY? 

## Follow Up: