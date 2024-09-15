# Decorator

Decorators are used to modify behavior of given function or class without directly modify it.

## How it works

A decorator is a high order function that take a function as argument and return a function.

```python
def a_decorator(func):
    def _subtitute(*args, **kwargs):
        return func(*args, **kwargs)

    return _subtitute

@a_decorator
def a_function(x):
   pass
```

This is equivalent to

```python
def a_function(x):
  print(x)

a_function = a_decorator(a_function)
```

When more than one decorators (`@d1`, `@d2`, .. `@dn`) are applied to a function `f` in that order, the result is the same as   `f  = d1(d2( ... dn(f))` (AKA stacked decorators).

## Parameterized decorators

Since a decorator would take the wrapped function as its sole parameter, to create a parameterized decorator, we would need to define a decorator factory. A decorator factory is a function that return the wanted decorator.

```python
def a_decorator(alternative_func=None):
    def _decorate(func):
        if alternative_func:
            return alternative_func
        return func
    return _decorate

@a_decorator(alternative_func=lambda _:True)
def a_function():
    pass

@a_decorator()
def a_function():
    pass
```

This is equivalent to

```python
a_function = a_decorator(alternative_func=lambda _:True)(a_function)
b_function = b_decorator()(b_function)
```

## Well-known decorators

### lru_cache

`functools.lru_cache` decorator is used to memorize function result in Least recent used manner, which discard the entries that have not been read for a while. Since `lru_cache` uses a dictionary to store the result, all arguments in the decorated function must be hashable. 

The decorator full signature is `functools.lru_cache(maxsize=128, typed=False)`, in that `maxsize` is number of maximum entries, `typed` is whether we should save value with same value but different types in different entries.

```python
@lru_cache()
def fibo(n):
    if n >= 2:
        return fibo(n-2) + fibo(n-1)
    return n
```

### singledispatch

`functools.singledispatch` decorator is used to create different function implementation for each data type. (which is overloading in other languages). When the function is executed, the implementation would be chosen based on type of the **first argument**.

Noted that the decorator is not designed to create function overloading, but for modular extension, means that each module can register implementations for its types.

```python
@singledispath
def a_function(obj)
    pass

@a_function.register(str)
def a_function_str(text):
    pass

@a_function.register(tuble)
@a_function.register(abc.MutableSequence)
def _(seq):
    pass
```
