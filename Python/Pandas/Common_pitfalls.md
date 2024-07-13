# Common pitfalls

# 

### Iterating in pandas

Iterating in pandas (including using `#apply()` method, which is just a fancier looping) is extremely slow, consider:

- Use a vectorized solution instead of looping
- If vectorization is not possible, using `#itertuples()` if it not required modifing and `#iterrows()` if it is. Method `#itertuples()` is substantially faster than `#iterrows()` and also preserve the row data types. 

```python
for index, row in df.iterrows():
  name = row['Name']

for row in df.itertuples():
  index = getattr(row, 'Index')
  name = getattr(row, 'Name')
```

### Appending to `Dataframe`

Using `#concat()` for appending row to the existing `Dataframe` is extremely slow. 
Try appending to a list then create the `Dataframe` from it would be more efficient.

```python
new_df = pd.DataFrame()
for row in df.itertuples():
  row = pd.DataFrame({"name": [row.name], "age": [row.age]})
  new_df = pd.concat([new_df, row], ignore_index=True)
```

```python
new_list = []
for row in df.itertuples():
  row = [row.name, row.age]
  new_list.append(row)
new_df = pd.DataFrame(new_list, columns=["name", "age"])
```

 

### Using `#apply()`

The `#apply()` method is just a fancier looping in pandas, which is quite slow and should be avoided.

The pandas column would return a NumPy's series, which we can apply Numpy operations to => We can use this as a replacement for `#apply()`

```python
df['Category'] = np.where(df['Age'] < 60,  'Elder', 'Young')
```

```python
# sales and profit are Numpy's series
def _conditions2(sales, profit):
  pass

func = np.vectorize(_conditions2)
df["rank"] = func(sales, profit)
```
