# Introduction

## What is flyway

Flyway is the leading database migration tool.  
It can work as command-line, java api, maven plugin or gradle plugin.  
[Source](https://flywaydb.org/)

## How it works

Flyway using a schema history table named flyway_schema_history for manage version of the database.  
To migrate, Flyway will:

1. Scan the filesystem, or the classpath of the application for migrations which can be written in either sql or java.
2. Migrations will be checked against the schema history table, if their version number is lower or equal the current version, it will be ignored.
3. They will be sorted by version number and executed in order.
4. History table will be updated accordingly.
