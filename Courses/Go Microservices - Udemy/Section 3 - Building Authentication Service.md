[Links?](#)
[Embbed Videos?](#)
# Summary
----

# Related Stuff

----
# Notes:
- We created an authentication service that too uses chi, and chi middleware. 
- We added a users model. The author provided this code and I was advised to copy and paste. 
- We are using the `pgx` package as our database driver for postgres.
- We added postgres and our authentication service to the docker-compose yaml file.
- The author also said to download a sql script that creates the user table in the users db. I set up postgres db in db beaver to connect to the users database (the db we set as POSTGRES_DB in docker-compose.yml). I then executed the script from db beaver and it created the users table.
- We set up the broker service to have a new endpoint and handler to make a client call to the authentication service.
- We updated the `test.page.gohtml` to use fetch and make a post request to our new handler in our broker service (which makes a client call to our authentication service).

## Questions:
- What kind of encryption does the authentication service use?
```go
	err := bcrypt.CompareHashAndPassword([]byte(u.Password), []byte(plainText))

```
^ we used `bcrypt` from `golang.org` to store our hashed password in the database. We then check if our password is the value used to generate our hash stored in the database. If it is, we know the user has successfully logged in.

## Follow Up:
- Review encryption. 
- Review postgres
- Practice using postgres in golang
