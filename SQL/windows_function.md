# Windows function

### What is windows function

A **aggregate function** would calculate across a set of rows  and return a single rows.

```sql
select sum(salary) as sum_salary from employee
```

Similarly, a **windows function** would calculate across a set of rows but does not cause the aggregated value to be grouped into a single rows.

```sql
select name, sum(salary) over() sum_salary
from employee
```

### Syntax

```sql
windows_function_name (expression) over(
    partition_clause
    order_clause
    frame_clause
)
```

* windows function name is the name of the supported windows function, such as `sum`, `rank`, `row_number`, etc.

* partition clause divides rows into  partitions in which the function is applied. This is similar to **group by** clause. If it is not defined, the whole rows is treated as a single partition. 
  
  `PARTITION BY exp1, exp2`

* order clause specifies order of rows in a partition. Specify order clause would allow us to use some analytic function like `LEAD`, `LAG`, `FIRST_VALUE` or `LAST_VALUE`
  
  `ORDER BY expression [ASC|DESC] [NULL {FIRST|LAST}]`

* frame clause changes the frame which the function is applied to if we want to expand it out of current row

```sql
SELECT name,
       salary,
       month,
       SUM(revenue) OVER (PARTITION BY name, month
                            ORDER BY month
                            RANGE BETWEEN 2 PRECEDING AND CURRENT ROW
                          ) AS make_last_3_months_salary
FROM employee
```
