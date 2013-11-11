struct-create
=============

Creates Go source file of structs for use in some MySQL database packages. It uses [go-sql-driver/mysql](https://github.com/go-sql-driver/mysql) for querying the information_schema database. I created this for personal use, so it's not written for extensibility, but shouldn't be difficult to adapt for your own use.

Configuration may be set in the source file:
```
var defaults = Configuration{
	DbUser: "db_user",
	DbPassword: "db_pw",
	DbName: "bd_name",
	// PKG_NAME gives name of the package using the stucts
	PkgName: "DbStructs",
	// TAG_LABEL produces tags commonly used to match database field names with Go struct
	//members. This will be skipped if the string is empty.
	TagLabel: "db",
}
```

Or by a JSON file using the json flag `struct-create --json=test.json`
```
{
	"db_user": "db_user",
	"db_password": "db_pass",
	"db_name": "db_name",
	"pkg_name": "JsonTest",
	"tag_label": "db"
}
```

Sample output file:
```
package DbStructs

import (
	"time"
	"database/sql"
)

type Audit struct{
	Id int64	`db:"id"`
	User int64	`db:"user"`
	Subject string	`db:"subject"`
	SubjectId int64	`db:"subject_id"`
	Action string	`db:"action"`
	Content string	`db:"content"`
	Created time.Time	`db:"created"`
}

type Client struct{
	Id int64	`db:"id"`
	Status int64	`db:"status"`
	Name string	`db:"name"`
	ContactId sql.NullInt64	`db:"contact_id"`
	Street1 string	`db:"street_1"`
	Street2 string	`db:"street_2"`
	City string	`db:"city"`
	State string	`db:"state"`
	Zip string	`db:"zip"`
	Phone string	`db:"phone"`
	Fax string	`db:"fax"`
	UpdatedAt time.Time	`db:"updated_at"`
	CreatedAt time.Time	`db:"created_at"`
}

type Crew struct{
	Id int64	`db:"id"`
	Status int64	`db:"status"`
	TaskTypeCategoryId int64	`db:"task_type_category_id"`
	OfficeId int64	`db:"office_id"`
	LeadId int64	`db:"lead_id"`
	IsSubcontractor int64	`db:"is_subcontractor"`
	DisplayOrder int64	`db:"display_order"`
	WorkerCount int64	`db:"worker_count"`
	Name string	`db:"name"`
	Street1 string	`db:"street_1"`
	Street2 string	`db:"street_2"`
	City string	`db:"city"`
	State string	`db:"state"`
	Zip string	`db:"zip"`
	Phone string	`db:"phone"`
	Cell string	`db:"cell"`
	Fax string	`db:"fax"`
	UpdatedAt time.Time	`db:"updated_at"`
	CreatedAt time.Time	`db:"created_at"`
}

type Job struct{
	Id int64	`db:"id"`
	TractId int64	`db:"tract_id"`
	ClientId sql.NullInt64	`db:"client_id"`
	OfficeId int64	`db:"office_id"`
	JobHoldId int64	`db:"job_hold_id"`
	FieldManagerId sql.NullInt64	`db:"field_manager_id"`
	Lot string	`db:"lot"`
	Name string	`db:"name"`
	UpdatedAt time.Time	`db:"updated_at"`
	CreatedAt time.Time	`db:"created_at"`
}
```