# Decorator

Decorator is used to modify behavior of given function or class without directly modify it.

## How it works

In Python functions are first class objects, means that they can be: 

- Passed as arguments

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

- Returned from another function

```python
def create_adder(x):
  def adder(y):
    return x + y
  return adder

add_10 = create_adder(10)
print(adder(1)) # 11
```

Decorator will wrap the given function:

```python
def calculate_time(func):
     
    def wrapper(*args, **kwargs):
        begin = time.time()
        func(*args, **kwargs)
        end = time.time()
        print("Total time taken in : ", func.__name__, end - begin)
 
    return wrapper

@calculate_time()
def a_function(x):
  print(x)

# Equivalent to

def a_function(x):
  print(x)
a_function = calculate_time(a_function)
```
