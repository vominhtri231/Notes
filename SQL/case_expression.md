# Case expression

Case expression check each condition and return value the if first condition meet.

We can also define the default value with `else` . If not defined, `NULL` is returned.

```sql
SELECT 
OrderId,
CASE 
 WHEN Quantity > 30 THEN 'Big'
 WHEN Quantity < 10 THEN 'Small'
 ELSE 'Medium'
END AS Label
From Order;
```
