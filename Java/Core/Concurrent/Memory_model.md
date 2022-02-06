## Java memory model
![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-1.png)  
Each running thread have their own stack which contains methods it has called to reach to current point of execution. Each java program may have multiple thread and a heap.  
* Stack will contain all local variable (of primitive type and reference type). Data in the stack can not be shared between threads.
* Heap will contain all objects, their member variables and their static fields. Data in the heap can be shared between threads.

## OS memory model
![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-4.png)  
A model machine usually have multiple CPUs, which can have multiple cores.
Each CPU will have their own CPU registers, CPU caches to speed up the calculation.  
When the CPU need to write something else to the caches, the data in cache will be flushed back to the main memory. 

## The graph between Java - OS memory model
![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-5.png)
This model lead to 2 problems:
* Visibility of shared variable  
 When the cache is not flushed back to main memory, the shared variable may not be visible to other threads. 
  The `volatite` keyword will make sure that the variable will be read directly from the main memory and always written back when updated.
* Race condition  
 When 2 or more threads modify a share variable, it could lead to race condition.
  The `synchronized` keyword will make sure that only one thread can access the critical region.
  It also guarantees that every variable inside the synchronized block will be read from the main memory, 
  and get flushed back into memory when thread exits the block.



