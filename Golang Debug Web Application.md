[Links?](#)
[Golang - Go delve](https://www.jetbrains.com/help/go/attach-to-running-go-processes-with-debugger.html#attach-to-a-process-on-a-remote-machine)
[Go Delve - Go Tooling Workshop](https://github.com/campoy/go-tooling-workshop/blob/master/3-dynamic-analysis/1-debugging/1-delve.md)
[Debugging With Vim-Go](https://l-lin.github.io/2020-02-10-debug-with-vim-go/)
[Vim Go Debugging Tutorial](https://www.pavedroad.io/part-8-go-debugging-with-vim-and-delve/)
[Delve FAQ - Github](https://github.com/go-delve/delve/blob/master/Documentation/faq.md)
[Embbed Videos?](#)
<iframe width="560" height="315" src="https://www.youtube.com/embed/a1SneuI65O0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Summary

----
# Related Stuff
[[Go Tooling Workshop]]
[[Docker Delve]]

----
# Notes:
- I'm using `vim-go` debuggin capability.
- To debug non web applications, do:
```bash
dlv debug --headless --listen localhost:8181 --accept-multiclient --api-version 2 --log --log-output debugger,rpc ./cmd/web

```
- It's very important we don't use `--continue`.
- Then, from `nvim`, do `:GoDebugConnect localhost:8181`.
- Then, toggle break points in http handlers via `:GoDebugBreakPoint`.
- After we toggle our breakpoints, do `:GoDebugContinue`.
- As you can see, nothing has happened just yet.
- Then, do a `curl localhost:3000`. (port 3000 is for the web application I'm using). 
	- From `nvim` we can see that the debugging window jumped down to our toggled breakpoint.
- Some usefult settings in `vim-go`:
	- we can debug `go-debug` in vim go via:
	- `let g:go_debug = ['shell-commands']`
	- It's very useful to see what's being done under the hood via `vim-go`. It also exposed the debug command shown in the example above.
- To find process ids for a web application using a port use:
```bash
lsof -i :<port-number>
```
- To debug a non-web application:
```bash
dlv debug --headless --continue --listen localhost:8181 --accept-multiclient --api-version 2 --log --log-output debugger,rpc ./cmd/web

```
- This time, it's okay to use `--continue`, this will kick off the execution of our code. You could omit it like in the web application example. Either is fine. Just remember to use `:GoDebugContinue`.
- Some gotchas:
	- Go version matters. 
		- I have `go1.19` on my local machine. I kept getting issues. I installed `gvm` and then installed `go1.18`. I removed `dlv` from my `GOBIN` and reinstalled the dlv for `go1.18`. After that, I didn't have any of the problems I was receiving.
	- On my Linux machine, it's tough to attach a debugger to a running process:
		- [Article about why we can't](https://rajeeshknambiar.wordpress.com/2015/07/16/attaching-debugger-and-ptrace_scope/)
	- The article does suggest a workaround, but I kept getting a `Fsync error` when I tried modifying it, even with `sudo` . 
	- It looks like a workaround is to use Docker. I assume we have to build the exetubable as such:
```bash
go build -gcflags="all=-N -l" -o myApp
```
- Then  we have to move the binary into a docker container and also have delve installed (or build a base image with delve installed). I'm assuming we have to expose some ports for the container, one for the web application (if we are writing a web app) and one for the delve headless server.
	- Then we exec into the container, run the binary in detached mode. Then, do debug attach to that process.
	- Then, we can do a debug connect to the server from `nvim`.
### 2023-04-27 
### 16:39
- I configured my nvim dap with `nvim-dap-go`. I couldn't attach to the remote process. I found out that we have to tell which host and port we have to connect to. 
- After tell which host and port to connect to, I got a weird error in the repl console in `nvim-dap-ui`. It says the `port :8181 already in use` . I was still able to connect to it, but it caused weird behavior in the repl. I wrote up my findings in the commment in the repo:
  https://github.com/leoluz/nvim-dap-go/issues/35#issuecomment-1526728411
- I then forked the repo and experimented my findings:
  https://github.com/manofthelionarmy/nvim-dap-go/tree/experiment/go-headless-adapter
	- And it works :) 
 - This is exciting!! I may have my first open source contribution!!!!
 - I also see that they are only inserting into the dap configurations table if the config type was `go`. I changed that to also include `go_headless`:
```lua
  for _, config in ipairs(configs.dap_configurations) do
    if config.type == "go" or config.type == "go_headless" then
      table.insert(dap.configurations.go, config)
    end
  end
``` 
- Also notice something weird, the repl controls highlights aren't working, and I found the issue:
  https://github.com/rcarriga/nvim-dap-ui/issues/251
## 2023-04-29:
- I was wokring more on the repo I forked. I was Testing if `Debug`, `Debug Arguments`, and `Debug Package` were working. The first two work well, except for `Debug Package`:
```
[ DEBUG ] 2023-04-29T17:47:05Z-0700 ] ...rmando/.config/nvim/plugged/nvim-dap/lua/dap/session.lua:935 ]    1       {
  body = {
    category = "stderr",
    output = "Build Error: go build -o /home/armando/go/src/go-micro/__debug_bin -gcflags all=-N -l /home/armando/go/src/go-micro/front-end/cmd/web\ngo: cannot find main module, but found .git/config in /home/armando/go/src/go-micro\n\tto create a module there, run:\n\tgo mod init (exit status 1)\n",
    source = vim.empty_dict()
  },
  event = "output",
  seq = 0,
  type = "event"
}

```
- this is because of the current folder structure I have. It seems like the main module has to be in the same directory as the `go.mod`. Else, it recursively walks back to find the root of a `.git` project. 
	- This same issue affects the dap restart with this folder structure too.
	- This is a weird folder structure I'm using from the udemy class for microservices. I'm wondering if I would benefit if I used `goworkspace` feature in golang.

## Questions:
- If I use `go1.19` after I have installed `dlv` for `go1.18`, will `go1.19` ensure backward compatability for `dlv`?
- How can we debug cli applications?

## Follow Up:
- How to configure dap to do the same?
	- Take a look:
		- https://github.com/leoluz/nvim-dap-go
		- https://github.com/mfussenegger/nvim-dap/wiki/Debug-Adapter-installation#Go
		- https://github.com/mfussenegger/nvim-dap/wiki/Debug-Adapter-installation#go-using-delve-directly
- I should make a script that runs delve and takes input for which package I'm using, and additionally, any args to pass to the code I'm executing.
- May need to make some keybindings for nvim.
- Experiment and see if I can still run `go1.18` dlv when I use `go1.19`.