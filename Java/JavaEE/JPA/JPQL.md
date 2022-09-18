# JPQL

JPQL is the query language that allows you to defined database queries based on entity model.

Under the hook, JPA implementations will tranform the JPQL to SQL.

## Join fetch

`join fetch` would allow associates to be initialized along with the parent objects.
This would help if you need nested entity and avoid n+1 problem.

```java
@Query(value = "SELECT a FROM Author a INNER JOIN a.books b WHERE b.price > ?1")
List<Author> fetchAuthorsBooksByPriceInnerJoin(int price); 
```

```sql
SELECT 
  author0_.id AS id1_0_0_, 
  books1_.id AS id1_1_1_, 
  author0_.age AS age2_0_0_, 
  author0_.genre AS genre3_0_0_, 
  author0_.name AS name4_0_0_, 
  books1_.author_id AS author_i5_1_1_, 
  books1_.isbn AS isbn2_1_1_, 
  books1_.price AS price3_1_1_, 
  books1_.title AS title4_1_1_, 
  books1_.author_id AS author_i5_1_0__, 
  books1_.id AS id1_1_0__ 
FROM author author0_ 
INNER JOIN book books1_ 
  ON author0_.id = books1_.author_id 
WHERE books1_.price > ?
```

Using `join` would not have such effect but it will also produces the `join` part, which can filter out the invalid entries.
