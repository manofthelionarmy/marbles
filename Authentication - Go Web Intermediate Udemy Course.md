# Summary:
---
# Related Stuff:
---
# Notes:
- Trevor, the course instructor, goes over authentication in this lengthy module. I can't recall the difference between authenticating on the frontend and backend.
- I can't remember the part where we were providing some kind of authentication and it resulted in some weird edge case handling on the UI side. I need to find that video and review it.
	- This is covered in Section 6, lecture 81.
- Trevor goes over frontend authencation (sesh auth) and backend authentication (tokens) in Section 6, lecture 67.
- We used stateful tokens in the course. Review how we implemented it. I do recall that we were keeping track if the token had expired and did create a tokens table to persist the information regarding the token.
- We used the token and stored it in the session on the frontend. We then passsed the token in the request headers (the Authorization Header) as a bearer token. 
- We then evaluated the token on the backend to see if it had expired while also finding the user mapped to that token.
- We also hashed the password and token and stored them in the database. It was my first time using the crypto package to hash stuff. I need to learn why we had to do these steps in the first place.
- The last piece in the puzzle was creating an authentication middleware that protected routes on the backend. This authenctication middleware ensured if a token was passed to the backend and also is the real piece of code that actually evaluates the validity of the token.
- Next, we are going to protect routes on the frontend.
- How we protected the frontend routes was simple. We created middleware that simply checks if the session has a value called `userID`. We set the session when we submit the login form on the web application server. 
	- How we do this is we query the userID and hashed password given a user's email. We then compare hashedPassword to the password the user submitted in the login form. If they match, we store the users id in the session as `userID`. If the passwords don't match, we don't store the `userID` in the session.
 - Next, we'll handle logouts.