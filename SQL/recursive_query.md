# Recursive query

### Structure of recursive query

```sql
WITH cte_name (column_names) AS (
  -- Anchor
  SELECT ...
  UNION ALL
  -- Recursive
  SELECT ...
)
SELECT * FROM cte_name;
```

* The anchor part which selects the initial rows

* Union all combine anchor and recursive rows

* The recursive part which selects subsequence rows, we can limit the level of recursive here

### Examples

**Employees**

| EmployeeId | Name  | ManagerId |
| ---------- | ----- | --------- |
| 1          | Alice | NULL      |
| 2          | Bob   | 1         |
| 3          | Carol | 1         |
| 4          | David | 2         |
| 5          | Eve   | 4         |

```sql
WITH employee_hierarchy(EmployeeId, Name, ManagerId, Level) AS (
  -- Anchor
  SELECT EmployeeId, Name, ManagerId, 1 as Level
  FROM Employees
  WHERE ManagerID IS NULL
  UNION ALL
  -- Recursive
  SELECT e.EmployeeId, e.Name, e.ManagerId, eh.Level + 1 
  FROM Employees e
  INNER JOIN employee_hierarchy eh ON e.ManagerId= eh.EmployeeId
)
SELECT * FROM employee_hierarchy;
```
