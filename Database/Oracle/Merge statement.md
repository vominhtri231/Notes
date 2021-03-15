![](https://www.essentialsql.com/wp-content/uploads/2016/11/VISUAL-MERGE-DIAGRAM.png)


### Structure
``` sql
MERGE <target-table>
USING <source>
ON <match condition>
WHEN MATCHED
    THEN <update-statement>
WHEN NOT MATCH
    THEN <insert-statement>
WHEN NOT MATCHED BY SOURCE
    THEN <delete-statement>
```
* The source must not contain duplicated row (ORA-30926)
* All executing statements can have `where`
* Merge is optimized for set of data 
