# Summary:
# Related Stuff:
[[PCKE - Oauth]]
[[Oauth 2.0 Authorization Flow and OpenID connect]]
# Notes:
- When I left the app running and I went to eat, I came back and tried to search an artist. I got a nil pointer error, but it was because I wasn't handling the error. The error only returns from `models.GetArtists` if the client fails to hit spotify api. I have a feeling the token expired.
- I'm trying to reproduce this error, but I have to wait a while.
- I didn't get any errors if I'm using the app immediately after I authorized.
- I'm not sure if this error occured when I quit the app, and re ran it without having to re-authorize myself.
- Maybe my laptop logged out?
- Nevertheless, the next goal is to begin handling errors and make a modal of success/failure.