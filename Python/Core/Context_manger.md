# Context manager

## With statement

The with statement was designed to simplify the try/finally pattern, which will wrap the running block by setup and teardown method. This is very handy if we have some logic that must be run before/after such as a pair like open file then close it or change the arithmetic floating point when calculating and change it back.

```python
with open('abc.txt') as fp:
    src = fp.read()
```

## Context manager

The with statement must execute on a context manager object, which is a object that implement `__enter__` (get executed before) and `__exit__` (get executed after) method.

 The variable returned by `__enter__` method will be used in the optional `as` clause. 
 The method `__exist__` would contain exception type, value and traceback of the exception raised within the with block (they are`None` if no exception are raised). If the method return `True`, indicating that the exception is handled by the method, the exception will be suppressed, or else it will be re-raised.

```python
def __enter__(self):
    ...
    return a


def __exit__(self, exc_type, exc_value, traceback):
    ...
    if exc_type is ZeroDivisionError:
        return True
```

## contextmanager decorator

`@contextlib.contextmanager` decorator would help reduce the boilerplate when creating context manager. Python would create a corresponding context manager object for the generator function.

```python
@contextlib.contextmanager
def my_context_manager():
    # doing before logic
    try:    
        yield value_for_as_clause
    finally:
        # doing after logic
```

Noted:

* the `yield` must be wrapped inside a try/finally in order to make sure the after logic will get executed.

* contrast to context manager object, the `@contextmanager` function will suppress the exception by default, in order to re-raised it, we must explicitly catch and re-raise it again.


