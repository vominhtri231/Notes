# Operator overloading

Rules for operator overloading:

- Can not overload operators for build-in types

- Can not create new operators, only override existing one

- `is`, `and`, `or` and `not` operators can not be overloaded

## Unary operators

Those operators only take one argument: `self`.

Some unary operators are: `__neg__` ( `-x` ) , `__pos__` (`+x`), `__invert__`(`~x`), `__abs__`(`abs(x)`).

```python
def __neg__(self):
    return Vector(-x for x in self.values)
```

## Infix operators

Those operators that take 2 arguments, the first one is `self`.

Some infix operators are:

- `__add__` /`__radd__` for `x+y`

- `__mul__` / `__rmul__` or `x*y`

- `__eq__`/`__lt__` /`__gt__`/`__ge__`/ `__le__` / `__ne__` for comparison

```python
def __add__(self, other):
    pairs = itertools.zip_longer(self, other, fillvalue = 0.0)
    return Vector(a+b for a,b in pairs)
```

## Augmented assignment operators

Those operators that take 2 argument, the first one is `self` and will update the `self` value.

Some augmented assignment operators: `__iadd__` for `x+=y`, `__imul__` for x*=y.

In the case of missing matching augmented assignment operator, python will convert to infix operators and a assignment (`x+=y` would turn into `x=x+y`).

```python
def __iadd__(self, other):
    self.values = ...
    return self
```

## Noted

**- Unary and infix operators should return a new object, do not modify the input objects.**

**- Many operators would have fallback methods, for example the `__add__` /`__radd__` pair. If the operator override method can not handle the input, it should return a `NotImplemented` singleton value, not raising `NotImplementedError`, which will leave the door for other operator override methods get executed.**

**- Augmented assignment operators should not be defined for immutable class**
