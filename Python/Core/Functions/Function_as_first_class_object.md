# Function as first class object

## What is first class object ?

A first class object is a programing entity that can be:

* Created at runtime

* Assigned to a variable or element

* Passed as argument

```python
def shout(text):
  return text.upper()

def whisper(text):
  return text.lower()

def greet(text, func):
  print(func(text))

greet("Hello", shout) # HELLO
greet("Hello", whisper) # hello
```

* Returned as the result

```python
def create_adder(x):
  def adder(y):
    return x + y
  return adder

add_10 = create_adder(10)
print(adder(1)) # 11
```

In python, Functions are first class objects

## High order function

A function that take a function as argument or return a function as the result are called High order function

```python
students = ['Ann', 'Julia', 'Oliver', 'Bob']
sorted(students, key = len)
```

Here the sorted function is a high order function that take `len` function as argument to sorted student by their name's length.

Some well-known high order function in functional paradigm are `map`, `reduce`, `filter` and `apply`, which available in python. However, `apply` is removed in later versions and `map`, `reduce`, `filter` have better alternatives for them such as list comprehension and other aggregated function such as `sum`, `any`, or `all`.

## Anonymous function

The use of high order function also require creation of small, one-off function, which is why anonymous function is created.

```python
students = ['Ann', 'Julia', 'Oliver', 'Bob']

sorted(students, key = lambda name: name[::-1])
# the lambda funciton would create a function as
def reverse(name):
    return name[::-1]
sorted(students, key = reverse)
```

The lambda function can only contain a expression, no statements allowed.
