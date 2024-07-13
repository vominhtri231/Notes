# Data types

## `DataFrame`

The main data type in Pandas is `DataFrame`, which is a 2D data structure with rows and columns, just like a data sheet in excel.

```python
df_students = pd.DataFrame({
    "Name": ["Anna", "Bob"],
    "Age": [12, 14],
    "Score": [6, 7]
})
```

## `Series`

Each column in a `DataFrame` is a`Series`. A `Series` would have no row labels, only a single column label.

```python
names = df_students["Name"] // series of names

ages = pd.Series([33, 44, 55], name = "Age")
```

## Basic properties

- `shape`

For getting shape of a data frame or a series, returning a tuple

```python
df_students.shape // (2,3)
names.shape // (2,)
```

* dtypes

Get data types of columns

```shell
>>> df_students.dtypes
Name     object
Age       int64
Score     int64
dtype: object

>>> names.dtypes
dtype('O')
```
