[Links?](#)
[Embbed Videos?](#)
# Summary

----
# Related Stuff

----
# Notes:
### The Plan Moving Forward
- In the real world, we will be working with multiple tables in a database. 
- Therefore, we're going to desing multiple tables and work with them.
### Approaching Database Design
- Step 1:
	- search the web to see if someone has made a schema design based on the kind of application you're trying to build.
	- if you can't find any fall through to step 2.
- Step2:
	- Think of the kind of resources/data exist in your app. Think of this when you have made a mockup or ui/ux design of your application.
	- These features/resources should be separate tables.
- Step 3:
> Features that seem to indicate a relationship or ownership between two types of resources need to be reflected in our table design.
- Ex: An instagram clone.
- By taking a look at the resources provided in the app, relationships are drawn:
 ![[Pasted image 20230418201502.png]]
### One-to-Many and Many-to-One Relationships
- One to many:
	- examples:
		- a user *has many* photos.
		- a pokemon *knows/has many* moves.
		- a comedian *has many* tour dates
		- a plan *has many* parts
		- a book *has many* reviews
	- *has many* = *one-to-many* 
- Many-to-one:
	- converse of one-to-many
	- from the perspective of the "many".
	- examples: (darn these sound a lot like one-to-one)
		- a photo *has one* user. unlikely the same photo will be taken by a user.
		- a tour date (though there are several) *has one* comedian
		- a part *belongs to one* plane (tricky the same part can be used for other planes.)
		- a review for a book
	- think of it as a collection of resources tied to one entity. each item in the resource is unique, and has one owner, example a photo, a tour date.
	- *has-one* = *one-to-many*
## Questions:

## Follow Up:
