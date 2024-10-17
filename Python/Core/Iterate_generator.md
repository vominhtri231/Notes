# Iterate - generator

## For loop statement

Whenever interpreter need to perform a for loop on X (iterate over an object `X`), it would calls `iter(X)`.

```python
for value in X:
    print(value)

# equivalent to
it = iter(X)
while True:
    try:
        print(next(it))
    except StopIteration:
        del it 
        break
```

The build-in function `iter` would check whether the `X`  implements `__iter__` method and call it to obtains a `iterator`. If the `__iter__` is not implemented but `__getitem__` does, it would use the `__getitem__` function to create a iterator. If both functions are missing, a `TypeError` will be  raised. This behavior could cause a case that an object does not pass `issubclass(X, abc.Iterable)` but can be iterated over.  

The object that implement `__iter__` method are `iterable`. The `__iter__` method would create a iterator object, which is a object that implement `__next__` method. Iterators are designed that they can not be reused: you must rebuild a iterator by the `iter` function to re-iterate it.

## Generator

A generator is a `iterable`, which can be used in loop. Some way to create a generator object:

### Generator function

A generator function is a function that contains `yield` keyword, which will return a  generator object. Each `next` function call on the returned generator will execute the function and return the value at the `yield` and hang the function execution there  . The generator will raise `StopIteration` in the end of the function.

```python
words = [...]
def get_word_generator():
    for word in words:
        yield 2*word
```

Python also provide a set of generator functions in standards library, some well-known are: `filter`, `map`, `all`, `any`, `enumerate`, `zip`.

### Generator expression

A generator expression syntax just like a list comprehension, which will return a generator object from a given `iterable`. This could be very handy if the expression is short, if not, consider using generator function for readability.

```python
words = [...]
word_generator = (2*x for x in words)
```
