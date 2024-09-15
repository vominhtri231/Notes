# Signature

## Parameters

Python functions have extremely flexible parameters handling mechanism.

```python
def crete_student(name, age, *grades, cls=None, school=None, **attributes):
    pass
```

* name, age: positional or keyword parameters

* grades:  variable positional arguments which is a tuple of positional parameters. Positional arguments after defined positional parameters are captured by `*grades`

* cls, school: keyword only parameters (from python 3), which is those parameters defined after arguments prefixed with `*`. If you don't want to support variable positional arguments, just skip the argument name.
  
  ```python
  def simple_fn(a, *, b): 
      pass
  ```

* attributes: variable keyword argument which is a dictionary of keyword argument. Keyword arguments are not explicitly defined in the function signature are captured by `**atributes`

## Doc and annotation

Document of a function can be used to attach helper text to a function

```python
def simple_fn(a, b):
    '''A simple function'''
    pass
```

The doc will be stored under `__doc__` attribute of the function.

```python
simple_fn.__doc__
>> A simple function
```

From python 3 , annotation can be used to attach metadata to parameter of a function and its return value.

```python
def simple_fn(a: int, b: str) -> list:
    pass
```

Notice that no processing is done with these annotations. They are stored under `__annotations__` property of the given function and may be used by IDEs, linters, or frameworks.

```python
simple_fn.__annotations__
>> {'a': <class 'int'>, 'b': <class 'str'>, 'return': <class 'list'>}
```

## Introspect function signature

Since function can be treat as object, we can introspect its signature via its properties, such as `__defaults__` for its default parameters, `__kwdefaults__` for its default keyword only parameters, `__code__` for its arguments, variables, etc.

To simplify the work, we can also use `inspect` module.

```python
from inspect import signature

sig = signature(simple_fn)

for name, param in sig.parameters.item():
    print(param.kind, ":", name, "=", param.default)
```
