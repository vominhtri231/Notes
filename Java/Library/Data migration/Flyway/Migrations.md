# Overview
All changes to the database are called **migrations**. Can be writen in sql, java or script.   
There are 2 types of migrations:

### 1. Versioned migrations
Has a version (must be unique), a description and a checksum (to detect accidental changes). They are applied in order exactly once.  
There are:
1. Regular migrations: Used for creating tables, indexes, data updates, etc.
2. Undo migration: Used to undo the efffects of the versioned migarions

### 2. Repeatable migrations
Has a description and a checksum only. Instead of being run just once, they are applied every time their checksum changes, and after all versioned migrations.  
They are used for recreating views, procedures, functions, bull data reinserts, etc.

# Naming
The pattern for naming is:
* Prefix: V - for versioned, U - for undo, R for repeatable
* Version: Numbers with dots or underscores (Not for repeatable migrations)
* Separator: __ (two underscores)
* Description
* Suffix: .sql  
  Eg: `V2.1__Add_new_table.sql`, `R__Create_View.sql`

# Discovery
Flyway discover the migrations from multiple locations in the `locations` property. It could be:
* `classpath:` Eg: classpath:db/migration
* `filesystem:` Eg: /myproject/migration
* `s3:` - search AWS S3 buckets
* `gcs:` - serach Google Clound Storage buckets 