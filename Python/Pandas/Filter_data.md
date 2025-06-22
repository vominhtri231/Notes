# Filter `DataFrame`

## Filter specific columns

```python
# returns a series 
age_series = df_students["age"]  

# returns a data frame of 2 columns
age_name_df = df_students[["age", "name"]] 
```

## Filter specific rows

* Via numeric condition

```python
above_14 = df_students[df_students["age"] > 14]
```

The `df_students["age"]` expression would return a series of students age. A conditional expression like `>` , `<`, `==`, etc would result in a series of bool values.
Any series of bool values can be used to filter data frame's rows.

* combine condition

We can apply binary operation to bool series using `&` (and), `|` (or)  or `~` (not), **parentheses would needed**

```python
above_14_below_16 = df_students[(df_students["age"] > 14) | (df_students["age"] < 16)]
```

* filter by list of value

```python
df_students[df_students["name"].isin(['Anne', 'Bob'])]
```

If we need to filter by multiple columns

```python
df_students= df_students[df_students[['name', 'class']].isin(['Anne', 'A']).all(axis=1)]
```

```python
df_students= df_students[df_students[['name', 'class']].isin({'name': ['Anne', 'Bob'], 'class': ['A', 'B']}).all(axis=1)]
```

* Via special conditional expression

Beside conditional expression, we can use a bool series as mask series, such as `notna()`.

## Filter both rows and columns

Using `loc`/`iloc` for filtering both rows and columns.

Using loc if you need to filter via bool series.

```python
name_age_of_above_14 = df_students.loc[df_students["age"] > 14 , ["name", "age"]]
```

Using iloc if you need to filter via index:

```python
df_students.iloc[9:25, 2:5]
```

loc/iloc can also be used to assigned values.

## Get tail/head

```python
df_students.tail() # last 5 rows
df_students.tail(3) # last 3 rows
df_students.tail(-3) # last `number of row - 3` rows


df_students.head() # first 5 rows
df_students.head(3) # first 3 rows
```
