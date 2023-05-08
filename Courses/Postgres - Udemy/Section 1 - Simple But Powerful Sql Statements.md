[Links?](#)
[Embbed Videos?](#)
# Summary
- Section 1 was a pure intro to postgres sql.
- It went over creating tables, inserting data into tables, calculating columns within our queries, using string operators and functions.
- Postgres has its challenges:
	- writing efficient queries (more dependent on the user, and depends on the data)
	- desiging a schema (depends on the problem we're trying to solve or data we're trying to represent)
	- Postgres has advanced featurese and we must know when to to use them.
	- Managing/administering postgres in prod env can be challenging.
----

# Related Stuff

----
# Notes:
### What is postgresql all about?
- It stores information
- SQL is separate from databases. Postgres, MySQL, Oracle, etc are relational databses that support SQL.
- SQL stands for Structured Query Language and is used to communicate or interface with a database.
### Database Design Proces
![[Pasted image 20230408224142.png]]
### Creating Tables
[SQL Create Table Statement](https://www.w3schools.com/sql/sql_create_table.asp)
### Inserting Data into Table
[Insert Data Into Tables](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-insert/)
### Calculated Columns
- We can do math operations within a column. They will be evaluated and the value is captured in the resulting query. The column is returned as ?column? and we need to rename the column with `AS`.
Ex:
```sql
select name, population / area as population_density from cities;
```
### String Operators and Functions:
![[Pasted image 20230408222538.png]]
- there are string operators and functions I can use to manipluate string data.
- Example:
```sql
select name || ', ' || country as location from cities;

select concat(name, ', ', country) as location from cities;

select concat(upper(name), ', ', upper(country)) as location from cities;

select upper(concat(name, ', ', country)) as location from cities;
```
## Questions:
- What are the challenges of postgres?
	- Writing <mark style="background: #FFB86CA6;">efficient queries</mark> to retrieve information.
		- database are special servers and when they serve a request, it takes up resources. 
	- designing the <mark style="background: #FFB86CA6;">schema</mark>, or structure of the database
		- our data has a schema, and it can get complex when we are using relations
	- understanding <mark style="background: #FFB86CA6;">when to used advanced features</mark>
		 - every database has their own or similar set of advanced features.
	- <mark style="background: #FFB86CA6;">managing</mark> the database in a production environment
		- we need to run our database and have it highly available in production environemnets.

## Follow Up:
