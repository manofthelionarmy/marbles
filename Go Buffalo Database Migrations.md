[Go Buffalo Database Migrations](https://gobuffalo.io/documentation/database/migrations/)
[Database config for soda and buffalo](https://gobuffalo.io/pt/documentation/database/configuration/)
[Go Buffalo Pop](https://github.com/gobuffalo/pop)

# Summary:
- From the udemy course for Go Intermediate Web Applications, we are using the soda cli tool provided by the Go Buffalo framework. 
# Related Stuff:
[[What is a Persistance Layer, and Why should we have one?]]
[[A humble point of view on how to organize persistence in Go]]
#golang 

# Notes:
- We'll use the soda cli tooling for database migrations.
- To generate a configuration file with defaults:
```bash
soda g config
```

- To genreate a configuration for a specific kind of database:
```bash
soda g config --type <db>
```

```bash
# the -t, --type flag does this:
  -t, --type string   The type of database you want to use (cockroach, mariadb, mysql, postgres, sqlite3) (default "postgres")

```

- The supported Db's for the config are:
	- postgres
	- mariadb
	- mysql
	- sqlite3
	- cockroach
- The target directory is wherever we ran the command. It is better practice to hold this config and the migrations generated folder in a parent folder called migrations.