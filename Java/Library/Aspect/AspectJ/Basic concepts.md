# Join point
The point in the program flow where something happens.

It could be:
* When a method is called
* When exception is throw
* When a variable is set/get
* When an object is instantiated

# Point cut
Point cut define the way to capture the join point.

The structure of a point cut is: `pointcut pointutName(): thePointCut`  
Eg:
```java
pointcut callSayHello: call(* ABC.sayHello())
```

# Advice
Advice describe the crosscutting behavior.

There are 2 types of Advices: before and after.  
There are 2 interpretations that come after the after advice: After the join point executed successfully or after it throws an exception.

Eg:
```java
after() : callSayHello(){
    // crosscutting behavior here
}

after() returnning (Object obj): callSayHello() {}

after() throwing (Exception e): callSayHello() {}
```
