# Variable scope

* A variable that is assigned inside a function and is used inside it would have local scope

* A variable that is assigned outside of any function would have global scope

* A variable that is assigned inside a function but is used inside its nested function is called `free varible` and would have lexical scope

```python
c = 1

def f2():
    d = 2
    def f1():
        b = 3 
        print(b) # b would have local scope
        print(c) # c would have global scope
        print(d) # d would have lexical scope
```

Noted that Python would compile body of the function and decide which scope that a variable is in, no mater if the variable is defined before or not.

```python
b = 3
# Here b would have local scope,
# even though it is defined as global before
# This would make print statement fail since b is not defined 
def f1():
    print(b)
    b = 4
    
def f2():
    d = 2
    
    # Here b would have local scope,
    # even though it is defined before and should be a free variable
    # This would make print statement fail since d is not defined 
    def f1():
        print(d)
        d = 4
```

To make a variable `global` /`free` we could use `global` /`nonlocal` keyword

```python
# b is now a global variable
def f1():
    global b
    nonlocal c
    print(b)
    print(c)
    b = 4


def f2():
    d = 2
    
    # d is now a free variable
    def f1():
        nonlocal d
        print(d)
        d = 4
```


