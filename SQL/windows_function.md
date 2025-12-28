# Windows function

## What is windows function

A **aggregate function** would calculate across a set of rows  and return a single rows.

```sql
select sum(salary) as sum_salary from employee
```

Similarly, a **windows function** would calculate across a set of rows but does not cause the aggregated value to be grouped into a single rows.

```sql
select name, sum(salary) over() as sum_salary
from employee
```

## Syntax

```sql
windows_function_name (expression) over(
    partition_clause
    order_clause
    frame_clause
)
```

* windows function name is the name of the supported aggregate function, such as `sum`, `rank`, `row_number`, etc.

* partition clause divides rows into  partitions in which the function is applied. This is similar to **group by** clause. If it is not defined, the whole rows is treated as a single partition. 
  
  `PARTITION BY exp1, exp2`

* order clause specifies order of rows in a partition. Specify order clause would allow us to use some analytic function like `LEAD`, `LAG`, `FIRST_VALUE` or `LAST_VALUE`
  
  `ORDER BY expression [ASC|DESC] [NULL {FIRST|LAST}]`
  
  Noted that by specifying order clause, the calculation will happen on each row
  
  ```sql
  select id, sum(value) over()
  -- this will return same sum for all row, one calculation only
  from sales
  ```
  
  select id, sum(value) over(order by id)
  -- this will return cumulative sum for each row, each would have calculation 
  from sales

```
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

## Supported aggregate functions

### Lag

```sql
lag(expression [,offset] [,default] ) 
over ([partition_clause] order_clause)
```

* offset: number of row back from the current row, default 1

* default: the default value when offset is off the data range, if not defined, `NULL` will be returned

Example:

```sql
select 
   quota as currentSale,
   lag(quota) over (order by YEAR(time)) as previousSale
from sale
```
