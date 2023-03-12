[PCKE - Oauth](https://oauth.net/2/pkce/)
[PCKE Generator](https://example-app.com/pkce)
[PCKE RFC - How to calculate values](https://datatracker.ietf.org/doc/html/rfc7636#section-4.1)
<iframe width="560" height="315" src="https://www.youtube.com/embed/3OMENOsq2VA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Summary:
---
# Related Stuff:
#security 
#webapplications 
#golang 
#nodejs 

---
# Notes:
- The [PCKE Generator](https://example-app.com/pkce) provides a great example in how to generate the needed info for the pcke.
- This repo that this individual made has a great example of how to do the PCKE Generator implementation in go:
  [PCKE Example - Spotify Pkg - Brian Straunch Github](https://github.com/brianstrauch/spotify/blob/master/accounts.go)
- We need to generate a random string. We must use the `crypto/rand` package.
	- Example: [generate random string with crypto/rand - github gist](https://gist.github.com/dopey/c69559607800d2f2f90b1b1ed4e550fb)
- I don't know how random bytes is different from random string.
	- Also, why does our value have to be url safe?
	- URL Safe means base64 url encoding