# Loop

## Problems

`for` loop can cause a substantial amount of overhead after interpreted. Inside a loop:

* If there are function calls containing `dot`, these function references are evaluate each time it is called

* If there are global object accesses, these accesses can be substantially slower, since local accesses are much more efficient than global accesses

## Solutions

To remove the overhead of `for` loop, the we could use the map function or  list comprehension. We can think them as a `for` moved into C code.

If we stuck with a `for` loop, try reduce these function calls containing `dot` and global object accesses.
