# Reshape and pivot

## Data frame format

Data is usually put in "record" ("wide") format where there is one row for each subject or "stacked" ("long") format where there are multiple rows for each subject.  

This is a data of "long"" format, where there are multiple row for variable's value in a specific date

```xls
    value variable       date
0       0        A 2020-01-03
1       1        A 2020-01-04
2       2        A 2020-01-05
3       3        B 2020-01-03
4       4        B 2020-01-04
5       5        B 2020-01-05
6       6        C 2020-01-03
7       7        C 2020-01-04
8       8        C 2020-01-05
9       9        D 2020-01-03
10     10        D 2020-01-04
11     11        D 2020-01-05
```

## Pivot

To convert from "long" format to "wide" format, we can use **`DataFrame.pivot`** method.

```python
df.pivot(index="date", columns="variable", values="value")
```

This would result in this data frame of "wide" format, where there is one row for variable's value in a specific date.

```xls
variable    A  B  C   D
date                   
2020-01-03  0  3  6   9
2020-01-04  1  4  7  10
2020-01-05  2  5  8  11
```

**Notes:**

* pivot can only handle table with unique value in each row-column. If your data contains duplicated value, consider using `pivot_table` instead

* We can omit the `values` param in the `pivot` function, this will result in a data frame have hierarchical columns, whose topmost level are the respective value columns.

## Melt and wide_to_long

The top level function `melt` and `DataFrame.melt` method can be used to transform the given data frame to a format where:

- one or more columns are identifiers variables would keep their shapes 

- the rest are measured variables, are `unpivoted` to the row axis, leaving 2 columns: `variable` and `value`. These names are customizable via `var_name` and `value_name` parameters.

```python
  first last  height  weight
0  John  Doe     5.5     130
1  Mary   Bo     6.0     150
```

```python
people.melt(id_vars=["first", "last"], var_name="quantity")
```

```
  first last quantity  value
0  John  Doe   height    5.5
1  Mary   Bo   height    6.0
2  John  Doe   weight  130.0
3  Mary   Bo   weight  150.0
```

Similarly, we have the function `wide_to_long` which have more customize options for match columns.

## Stack and unstack

Similar to `pivot` and `melt`, for multiple indices data frame, we could use stack or unstack to handle them

- `stack`: pivot a level of column labels to inner-most row index

- `unstack`: pivot  a row index to inner-most column

Both 2 methods allow us to input parameter as column/index names, or number. If not provided, the inner most one would be used.
