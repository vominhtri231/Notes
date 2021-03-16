### Point cut types
* `call` is used to capture the method call and will weave the caller
* `execution` is used to capture the execution and will weave the executor
* `cflow` is used to capture all join points **under or equal** the specified point
* `cflowblow` is used to capture all join joints **under** the specified point
* `within` is used to capture join points under a class/package

```java
pointcut call_cflow_callA() :  cflow(call(* MyClass.callA()));
```

### Special character
```java  
// Using * to describe anything
// Using + after a type to describe anysubtype of a type
// Using .. in parameter to describe the method has 0 or more parameters.
pointcut callSetX()  : call(* (Point+).setX(..));
```

### Capture parameters
```java
    // Using args: define args on the method is called
    // Using target: define object on which the method is called
    // Using this: define object is currently weaved
    pointcut callMove(Object o,Point point, int dx, int dy) 
        : call(void Point.move(int,int))
            && args(dx,dy) 
            && target(point) 
            && this(o)
 
    before(Point point, int dx, int dy) : callMove(point, dx, dy )  {
    }
```