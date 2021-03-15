![](https://lh3.googleusercontent.com/pw/ACtC-3coJ2JIvdUH4Kvbr40ETqtw5iirLAiWqxmo9T0VGlWECxdFRtF6KCrDDf5N-UNbRqWNBi81yJrfty11xdW4SMHyiidIKzyQo0YcCvHl5V4zb5ccDIGfLsAK2tn318XsR3DvDXXlNYIWzbsDgo5_IZgx=w940-h736-no)

### Block
![](https://lh3.googleusercontent.com/pw/ACtC-3frjdOwu3ZIMKasRH1iV_GkrJkygYAM70IBE6hFXMDohIPYU0v162J541NAIlzTE-Jlfzk67p7gktRcq3zHgKXzw7VRuEzuh45aJUHXbYH1HOHdpZVdwIevIwaTLHd2JZUD4m7Yi9ixWjL9eNTRsNxO=w141-h243-no)

Block is a logical block, consist of several operating system blocks. Their size is preconfigured from 2-32KB (default 8KB).  
Block header contains block type (block saving rows or indexes), row directory (physical addresses of each row - ROWIDs), table information (the table(s) the block saving the data for).  
Data in a block is saved with space between them. You could use PCTFREE/PCTUSE to specify the space size. The more space means higher performace when editing a row but more spatial cost and vice versa.

### Extent

### Segment
There are 4 types of segments: Data, Index, Undo and Temporary. Temporay segment provides temporay work area.

### Tablespace
Used to group all related data in one container. There are 2 types of tablespace:
1. Temporay tablespace contains temporary data that only need to be stored in a session, stored in temporay files
2. Permanent tablespace stores persistent schema objects, stored in data files.
   Each database must have at least 2 tablespaces: SYSTEM and SYSAUX.

### User vs Schema
* In oracle, a schema is a collection of database objects own by a user. __A user owns a schema and have the same name__.
* The `CREATE USER` command creates user and a schema for that user. As well as `DROP USER` will delete both user and schema.
* the `CREATE SCHEMA` command __does not create a `schema`__ as it implies.