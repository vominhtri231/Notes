# Cross apply

Cross apply is used to join a table with a table-values function or a correlated subquery. It will evaluate right side table expression for each row and will return join row if matched.

## Example:

### Apply to correlated subquery

For each category, cross apply will execute the correlated subquery to retrieve the top 2 product.

```sql
SELECT 
  c.name,
  r.product_name,
  r.price
FROM 
  categories c
  CROSS APPLY (
    SELECT TOP 2 *
    FROM product p 
    ON p.category_id = c.category_id
    ORDER by p.price
 ) r
```

### Apply to table-values function

Defined a table-values function to retrieve the top 2 product by category id

```sql
CREATE TABLE GetTopProductsByCategory(@category_id INT)
RETURN TABLE
AS RETURN (
    SELECT TOP 2 *
    FROM product p 
    ON p.category_id = c.category_id
    ORDER by p.price
)
```

```sql
SELECT 
  c.name,
  r.product_name,
  r.price
FROM 
  categories c
  CROSS APPLY GetTopProductsByCategory(c.category_id) r
```


