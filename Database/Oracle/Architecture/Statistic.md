# System statistic
The statistic used to estimate the cost of CPU and I/O. If there are no system statistics, the DB will assume that the machine will read an I/O block in 12 seconds.   
It sould be gatherd regularly, especially when there are a hardware change, by:
```SQL
    -- ALL required system privilage
    EXEC DBMS_STATS.GATHER_SYSTEM_STATS('Start');
    SELECT * FROM SYS.AUX_STATS$;
```
# Optimizer statistic
The statistic contains information about the database objects like tables, indexes, columns, etc. It can be gatherd automatically or manualy, or using dynamic statistic. You may want to gather optimizer statistic manully when the DB structure change, or the automatic gathering can not run for all the objects (it's a very costly operation).


### Get optimizer statistic
The old way of gathering optimizer statistic (not recommended, only kept for backward compatible) would be:

```SQL
ANALYZE TABLE <table_name> COMPUTE STATISTICS;
``` 

The modern ways:
```SQL
EXEC DBMS_STATS.GATHER_DATABASE_STATS();
--- Gather statistic for dictionary schemas (e.g SYS, SYSTEM schemas)
EXEC DBMS_STATS.GATHER_DISTIONARY_STATS();
EXEC DBMS_STATS.GATHER_SCHEMA_STATS(ownname=>'SH');
-- If cascade is true, the db will generate statistic for all indexes of that table.
EXEC DBMS_STATS.GATHER_TABLE_STATS(ownname=>'SH',tabname=>'SALES',cascade=>'true');
EXEX DBMS_STATS.GATHER_INDEX_STATS(ownname='SH',indname='IDX_SALES_ID');
```

Optimizer statistics is saved in those views: X_TABLES, X_TAB_STATISTICS, X_TAB_COL_STATISTICS, X_INDEXES, X_CLUTERS, X_PARTITIONS, X_IND_PARTITIONS, X_PART_COL_STATISTICS, etc.  
The X can be DBA (all statistics of the db), USER (statistics for the tables owned by the user), or ALL (statistics for the tables accessible to the current user).
### Type of optimizer statistic
1. Table statistic: Number of rows, number of blocks
2. Column statistic: Number of distinct values, number of NULL values, data distributed statistics (Aka Histogram - selectivities of columns), extended statistic (Logical relations of columns)
3. Index statistic

### Dynamic statistic
When the statistic is missing or insufficent,etc the DB may query some sample block to get statistic at __parse time__.  
The level for dynamic statistic is from 0 - Not get any sample  to 10 - get all blocks (Default is 2 for automatic sampling). This can be set in system level, session level or query level `dynamic_sampling(1)`. The higher level of estimation means more CPU cost but more accurate estimation.