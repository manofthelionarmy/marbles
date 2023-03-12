# Summary:
# Related Stuff:
[[Spotify, Bubble Tea Golang TUI project]]
[[PCKE - Oauth]]
# Notes:
- I did a poc for how to do client credentials and get hooked up to spotify via a cli.
- I then used Brian Straunch's `spotify-cli` project as reference and saw that he used PCKE. 
- I looked up the PCKE documentation on Oauth2.0's website and looked at the PCKE specification for how to generate the code verifier and code challenge.
	- I learned how to use the `crypto/rand` package, which is better to use for encryption/cryptogarphy over `math/rand`.
 - To generate the code_verifier, I had to follow the PCKE specification and build a random string from the characters only allowed, as stated by the specification.
 - To generate the code challenge, I had to do sha256Sum of the code verifer and then base64 url encode it.
 - I also had to generate a random `state` value via `crypto/rand`. It's purpose is to prevent/guard against CSRF, and pretty much, I said a random `state` value in my request. And, when the flow hits my redirect uri as a webhook, I then have to check the state the sent in my request. If it doesn't match the random state I generated, then that means that it's a CSRF and imediately shutdown the program. If it's not, then that means it's not a CSRF and we're good to get the token in the exchange.
 - After that, I began working a bit with `github.com/zmb3/spotify/v2` package to better understand it and get familiar with it.
	 - I had to use the spotify documentation and learned when I do the search, I should url encode my query and I'll get back better results.
 - I began using the bubble tea package and did a POC to understand it.
 - They have simple abstractions. The main one is a `Model`, which contains or encapsualtes state within the TUI application pertaining to that model. As a model, it can also display a view or capture events and update the state. Messages (events) trigger updates and we can modify our state based on these events.
 - We can do composite models, meaning we can have two or more models render in the same window. We then have to return `tea.Batch([]tea.Cmd{}...)`.
 - `tea.Cmd` is another abstraction, and this is from there docs:
   [Commands and Messages](https://github.com/charmbracelet/bubbletea/tree/master/tutorials/commands#commands-and-messages)
> `Cmd`s are functions that perform some I/O and then return a `Msg`. Checking the time, ticking a timer, reading from the disk, and network stuff are all I/O and should be run through commands. That might sound harsh, but it will keep your Bubble Tea program straightforward and simple.
- `tea.Cmd` is very critical in `tea.Model.Update`:
[Update - tea.Model](https://github.com/charmbracelet/bubbletea/tree/master/tutorials/commands#the-update-method)
> Internally, `Cmd`s run asynchronously in a goroutine. The `Msg` they return is collected and sent to our update function for handling. Remember those message types we made earlier when we were making the `checkServer` command? We handle them here. This makes dealing with many asynchronous operations very easy.
- It's very important that if we have composite models, we invoke their update function within the containing model.
	- This ensures that messages get picked up by these models and we don't get a frozen screen.
 - Another value that gets returned from `tea.Model.Update` is another `tea.Model`. In fact, it is the `tea.Model` itself it returns with updated state, for example:
 ```go
// msg is a tea.Msg
listModel, cmd = listModel.Update(msg)
```
- From this update, we can return another model than the model itself. 
- This will make it possible to have a ui that renders other *views* or *layouts* within the terminal.