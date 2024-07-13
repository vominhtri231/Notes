# Group by

## Grouping

Group data to categories

```python
df = pd.DataFrame({'Animal': ['Falcon', 'Falcon',
                              'Parrot', 'Parrot'],
                   'Max Speed': [380., 370., 24., 26.]})
```

```python
df.groupby(['Animal']).mean()
```

```xlsx
        Max Speed
Animal
Falcon      375.0
Parrot       25.0
```


Some supported aggregate functions:

* count()

* sum()

* mean()

* median()

* min()

* max()

* mode()

* std() - standard deviation

* var() - variance

* agg() - for flexible aggregation
  
  ```python
  df.groupby('a').agg({'b':lambda x: list(x)})
  ```

## Explode

Transform each list-like element to a row, replicate index values. We have the option to ignore the index and reindex the result.

```python
df = pd.DataFrame({'A': [[0, 1, 2], 'foo', [], [3, 4]],
                   'B': 1,
                   'C': [['a', 'b', 'c'], np.nan, [], ['d', 'e']]})
```

```python
df.explode('A')
```

```xlsx
     A  B          C
0    0  1  [a, b, c]
0    1  1  [a, b, c]
0    2  1  [a, b, c]
1  foo  1        NaN
2  NaN  1         []
3    3  1     [d, e]
3    4  1     [d, e]
```
