# Fanout

SQL-fanout is the situation where we combine join and aggregate function (sum, count, avg, etc), these 2 concepts can interact and produce wrong result due to duplicate cells.

A **N-N** or even **1-N** join can multiply a row, which if we apply the aggregate function, may produce wrong result. 

## Example

Table **customer**

| customer_id | name |
| ----------- | ---- |
| 1           | Jean |
| 2           | Bob  |
| 3           | Anne |

Table **order**

| order_id | amount | customer_id |
| -------- | ------ | ----------- |
| 1        | 25     | 1           |
| 2        | 50     | 1           |
| 3        | 75     | 2           |
| 4        | 100    | 3           |

Table **visit**

| visit_id | customer_id |
| -------- | ----------- |
| 1        | 1           |
| 2        | 1           |
| 3        | 2           |
| 4        | 3           |

If we want a SQL of customer with him/her order amount and number of visit

```sql
select sum(o.amount), count(v.visit_id)
from customer c
left join order o on c.customer_id = o.customer_id
left join visit v on v.customer_id = c.customer_id 
```

| customer_id | name | order_id | amount | visit_id |
| ----------- | ---- | -------- | ------ | -------- |
| 1           | Jean | 1        | 25     | 1        |
| 1           | Jean | 1        | 25     | 2        |
| 1           | Jean | 2        | 50     | 1        |
| 1           | Jean | 2        | 50     | 2        |
| 2           | Bob  | 3        | 75     | 3        |
| 3           | Anne | 4        | 100    | 4        |

As we can see, as join multiple the matching cells the amount sum multiple time and not correct anymore 

## How to prevent

To prevent from the root of the problem, we must analyze the characteristic of the join, will it fanout or not. (**1-N** , **N-N**)

If it does, move aggregate function to the to be grouped part => change the characteristic of join to **1-1**, which will not cause fanout.

For the example above:

```sql
SELECT 
  c.customer_id,
  c.name,
  o.total_amount,
  v.total_visits
FROM customer c
LEFT JOIN (
  SELECT customer_id, SUM(amount) AS total_amount
  FROM "order"
  GROUP BY customer_id
) o ON c.customer_id = o.customer_id
LEFT JOIN (
  SELECT customer_id, COUNT(*) AS total_visits
  FROM visit
  GROUP BY customer_id
) v ON c.customer_id = v.customer_id;
```
