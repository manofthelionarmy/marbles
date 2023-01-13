[Add Column](https://gobuffalo.io/documentation/database/fizz/#add-a-column)
[Drop Column](https://gobuffalo.io/documentation/database/fizz/#drop-a-column)
[Fizz](https://gobuffalo.io/documentation/database/fizz/#fizz)
# Summary:
- This is something I learned how to do during the udemy course, Go Intermediate Web Applications
# Related Stuff:
# Notes:
- Command I ran:
```bash
soda generate fizz AddImageToWidgets
```
- In the above, we were adding a new column. More about how to do this:
	[Add Column](https://gobuffalo.io/documentation/database/fizz/#add-a-column)
- We have to add this statement to the migration file generated (the `up` migration file):

```javascript
add_column("table_name", "column_name", "string", {})
```

- Fizz is a DSL (and the DSL script's language is Javascript).
- Now that we've added to our `up` migration, we must add to our down migration by  dropping the column
```javascript
drop_column("table_name", "column_name")
```