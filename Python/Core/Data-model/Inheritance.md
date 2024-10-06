# Inheritance

## Protocol

Protocols are informal interface, which include set of public attributes (method and data attributes). They are defined only in document and unenforced.

For example, the sequence protocol entails `__getitem__` and `__len__` methods. Any class that implements those two methods can be used as a sequence. We call it a sequence because it behaves like one. This is known as **Duck Typing**.

Since it is informal, we can also implement a part of the interface,  if we known how the class will be used. For example, if a class only used in iteration, only `__getitem__` is required.

## ABC

Beside protocol, we can create a base class and subclass it. If the base class's meta class is `abc.ABCMeta`, we are guaranteed that the subclass will conform the base class signature and making the interface more official. 

This can become handy if we need to create a extensible system or framework, we user can input their class implementations. In other cases, this can be a bad choice and we should avoid create our ABC classes.

### Example

```python
class XMap(abc.ABC):

    @abc.abstractmethod 
    def read():
        pass

    def can_read():
        try:
            read()
            return True
        except:
            return False
```

An ABC subclass has to implement all its abstract methods, or an exception will be thrown when the class is constructed.

### Virtual subclass

We can even register a virtual subclass of an ABC, even when it does not actually inherit from it.

```python
@XMap.register
class VirtualXMap:
    def read():
        pass


# Or we can do: XMap.register(VirtualXMap)
```

This way, the program will consider the virtual subclass is a subclass of the ABC, if we check it via `issubclass` or `isinstance`. Noted that if the registered class is not conformed the base class signature, it will experience unwanted behaviors.

### Subclass hook

In some cases, a ABC class may automatically check if a class is its subclass or not, via checking its API in `__subclasshook__` method.  This approach is actually chosen by the Go language. For example the Sized ABC class. 

```python
@classmethod
def __subclasshook__(cls, C):                
    if cls is Sized:
        if any("__len__" in B.__dict__ for B in C.__mro__):
            return True
    return NotImplemented
```

## Subclassing build-in types

In `CPython`,  due to the fact that build in types like `list`, `dict` or `str` implementation are written in C language for performance purpose, their behaviors violate the basic rule of OOP: the search of method should always start from the class of the target instance. This makes subclassing build-in type in `CPython` result in non-deterministic behaviors. 

This is intentional for optimize performance. To subclass a build-in, python provides the extensible type like `UserDict`, `UserDict` or `UserString`. These types are not as speedy as the build-in types, but will work as expected when they are subclassed.

Noted that this only happens in `CPython`, if you using `PyPy` you will not experience it.

```python
class DupleDict(dict):
    def __setitem__(self, key, value):
        super().__setitem__(key, value * 2)

dd = DupleDict(one=1)
dd['two'] = 2
dd.update(three=3)
# dd is now {'one': 1, 'two': 4, 'three': 3}
```

## Multiple inheritance - method resolution order

 Python allow multiple inheritance. In the below example, class A inherit from B, C and D class.

```python
class A(B,C):
    pass
```

To identify which method/attribute to use for a instance, Python would use the method resolution order, which can be access via `__mro__` function. This indicate the order that we will look for the method/attribute.

```python
A.__mro__
# (<class '__main__.A'>, <class '__main__.B'>, <class '__main__.C'>, <class 'object'>)
```
