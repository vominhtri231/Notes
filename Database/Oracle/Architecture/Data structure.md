![](./img/logical_physical_dbs.jpg)

### Block
![](./img/database_block.png)

Block is a logical block, consist of several operating system blocks. Their size is preconfigured from 2-32KB (default 8KB).  
Block header contains block type (block saving rows or indexes), row directory (physical addresses of each row - ROWIDs), 
table information (the table(s) the block saving the data for).  
Data in a block is saved with space between them. You could use PCTFREE/PCTUSE to specify the space size. 
The more space means higher performance when editing a row but more spatial cost and vice versa.

### Extent

### Segment
There are 4 types of segments: Data, Index, Undo and Temporary. Temporary segment provides temporary work area.

### Tablespace
Used to group all related data in one container. There are 2 types of tablespace:
1. Temporary tablespace contains temporary data that only need to be stored in a session, stored in temporary files
2. Permanent tablespace stores persistent schema objects, stored in data files.
   Each database must have at least 2 tablespaces: SYSTEM and SYSAUX.

### User vs Schema
* In oracle, a schema is a collection of database objects own by a user. __A user owns a schema and have the same name__.
* The `CREATE USER` command creates user and a schema for that user. As well as `DROP USER` will delete both user and schema.
* the `CREATE SCHEMA` command __does not create a `schema`__ as it implies.