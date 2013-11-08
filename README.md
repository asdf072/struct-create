struct-create
=============

Creates Go source file of structs for use in some MySQL database packages. It uses [go-sql-driver/mysql](https://github.com/go-sql-driver/mysql) for querying the information_schema database. I created this for personal use, so it's not written for extensibility, but shouldn't be difficult to adapt for your own use.

Set your configuration in the const section:
```
const (
	DB_USER     = "my_user"
	DB_PASSWORD = "pAsswor3"
	DB_NAME     = "my_db"
	// PKG_NAME gives name of the package using the stucts
	PKG_NAME = "DbStructs"
	// TAG_LABEL produces tags commonly used to match database field names with Go struct members. This will be skipped if the string is empty.
	TAG_LABEL = "db"
)
```