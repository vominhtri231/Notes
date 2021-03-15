## Creating index
* The indexes is saved in `user_indexes`
* Can not have more than 1 active index for the same set of columns
* Creating unique constraint would also create unique index but not always. If there is an index exists, no index will be created, no mater the index is unique or not.
* If there is a change in table structure, the index may out of date and need to be rebuild.
```sql
ALTER INDEX <index-name> REBUILD;
```
* The index could be made invisible, for checking the performance, but the database still maintain it.
```sql
ALTER INDEX <index-name> INVISIBLE; --or VISIBLE
```

## Attributes of index
* Reverse: reverse the bit of column value to use as node value => should be used for auto increase column with a lot of insert/update + can not be used for range scan.
* Key compression
* Order (Eg: Ascending, decending)
* Unique
* Composite: index with multiple columns, the more left one should be more queried and more selective.
* Compress: based on __duplicate columns__ to reduce the disc size => improve performance. If there is not too much duplicate, the performance will be decreased.

## There are 2 types of indexes
1. B-Tree(Balance tree)

![](https://docs.oracle.com/cd/E11882_01/server.112/e40540/img/cncpt244.gif)

* The indexed column should have high selectivity
* B-tree indexes will not index the NULL values and will store values in order
* Can be compressed

2. Bitmap

![](https://www.oreilly.com/library/view/oracle-essentials-oracle9i/0596001797/tagoreillycom20070221oreillyimages76620.png)

* The indexed column can have low selectivity, and the data not modified too often
* The performance of index is high if combine multiple conditions since it could combine result with other indexes (bitmap or not - in case of tree index, the rowid would be converted to bitmap)
* Bitmap index will index the NULL values but will not store values in order.
* Can choose the partition (LOCAL vs GLOBAL)
* Can have multiple tables index (Bitmap join index) to speech up the joining

## Using indexes

* The index columns should stand clearly, without any arithmetic/ concatenation operation, in order to make the optimizer chose to use the index.
* If you really need the function with the column, should consider using function base indexes.
* If using `LIKE` operation, the wildcard should not be on the start of the string. It would prevent the optimizer to use the indexes. If you really need to search to last chararecters, consider creating indexes combine with reverse function.
* B-tree indexes will not index the NULL value => using NULL value may suppress the usage of index. To fix this, we may try to add constraint or add `is not null` predicate or using bitmap indexes instead.
* If the data types are mismatch, it required to have a implicite cast => may suppress usage of indexes.