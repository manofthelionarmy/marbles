[SCS golang package](https://github.com/alexedwards/scs)
# Summary:
- We used this package for session management in the go intermediate web programming course.
# Related Stuff:
#golang 
[[How to Add a Column with Fizz and Soda Cli]]
[[Go Buffalo Database Migrations]]

# Notes:
- The use case for this came along because we don't want to resend the form on a page reload. This can charge the user more than once. We instead want to do a http redirect after submitting the form. Before we do a http redirect, we want to save some information before the next page renders. This is the use case for session management.
## Follow Up:
- Learn the basics of session management.