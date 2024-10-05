# `Dunder`

Data model in python formalizes the interface of the building block of the language like iterators, context managers, operations, string format, etc. As if the python language is a framework, we may need to implement methods that will be called by the language.

For example, by implementing `__getitem(key)__` of a class, we support the syntax `obj[key]` on the class's instances.

These special methods name is wrapped inside double underscore `__xyz__`, AKA `dunder` methods.  
**Note**: Should not name a user defined method like `dunder` method, since the name may be used in the future release.

These methods should not be called by the program directly, except for the `__init__` method , to initialize the superclass in your own `__init__` implementation.

Some well-known `dunder` methods:

* `__new__`, `__init__`, `__del__` for instance creation and deletion

* `__hash__` and `__eq__` for using objects in set/dictionary and override `=` operator

* `__enter__`, `__exit__` for context management

* `__call__` for emulates functions

* `__repr__`, `__str__`,`__format__`, `__bytes__` for presentation

* `__get__`, `__set__`, `__delete__` for attribute descriptor

* `__iter__` , `__reversed__`, `__next__` for iteration

* `__getattr__`, `__setattr__`, `__delattr__`, `__dir__` for attribute management

* `__len__`, `__getitem__`, `__setitem__`,`__delitem__`, `__contains__` for emulating collections

* `__neg__` (-), `__pos__` (+), `__lt__` (>), etc for emulate operators
