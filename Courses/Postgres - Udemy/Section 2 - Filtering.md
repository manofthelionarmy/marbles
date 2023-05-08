[Links?](#)
[Where Clause - Postgres Tutorial](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-where/)
[Update Statement - Postgres Tutorial](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-update/)
[Embbed Videos?](#)
# Summary

----
# Related Stuff

----
# Notes:
- We are using the WHERE clause.
- We can filter with the where clause using comparison operators:
![[Pasted image 20230410192129.png]]
- IN, BETWEEN, and NOT are comparison operators.
- We can COMPOUND operators to form more complex queries via AND and OR.
```sql
select name, area from cities where area > 4000;

select name, area from cities where area = 8223;

select name, area from cities where area != 8223;

select name, area from cities where area <> 8223;

select name, area from cities where area between 2000 and 4000;

select name, area from cities where name in ('Delhi', 'Shanghai');

select name, area from cities where name not in ('Delhi', 'Shanghai');

select name, area from cities where area not in (3043, 8223) or name = 'Delhi';

select

name, area from cities

where

area not in (3043, 8223)

or name = 'Delhi'

or name = 'Tokyo';
```
- Not only can we do mathematical and string operations in our queries, we can also use them within our where clauses.
- However, we can't refer to the column calculation within our where clause. It's like they are scoped from one another.
- Use Where Clauses in our update statements to tell the db which tuple/record we want to update.
	- Make sure where clause targets a unique entry or be careful and specific (I wonder if we can perform multiple updates based on a reoccuring value like update all torn pants in a dresser to patched).
 - Delete is a statement that lets us delete a record/tuple in a database based on an attribute via the where clause, similar to how update lets us update based on the where clause.
	 - Be careful, we can delete multiple entries from a db with a similar value. 
	 - You can delete one tuple based on a value that is unique.
```sql
update cities

set population = 39505000

where name = 'Tokyo';

delete from cities where name = 'Tokyo';
```
## Questions:
- How can we update multiple columns/attributes in a databse?
```sql
UPDATE table_name
SET column1 = value1,
    column2 = value2,
    ...
WHERE condition;
```

## Follow Up:
