Eg: Let say we have a stack
```java
	public class Stack<E> {
     	public void push(E e);
        public E pop();
        public boolean isEmpty();
    }
```
```java
    Stack<Number> numberStack = new Stack<>();
	Iterable<Integer> intergers = ...
	numberStack.pushAll(intergers)

	// this won't work
    public void pushAll(Iterable<E> src){
        for(E e: src) push(e)
    }

	// but this does
	public void pushAll(Iterable<? extends E> src){
        for(E e: src) push(e)
    }
```
```java
    Stack<Number> numberStack = new Stack<>();
	Collection<Object> objects = ...
	numberStack.popAll(objects)

	// this won't work
    public void popAll(Collection<E> dst){
        while(!isEmpty()) dst.add(pop());
    }

	// but this does
	public void popAll(Collection<? super E> dst){
        while(!isEmpty()) dst.add(pop());
    }
```
=> To maximun flexibility use wildcard types on input paramerters that represent producer or consumer. The simple rule is: ***PECS - PRODUCER EXTEND, COMSUMER SUPER***

### Remark
1. A proper use of wildcard types, they are nearly invisible to user of the class. If user of a class has to think about wildcard type that means something wrong with the API  
   => should not use wildcard type as return type because it force user to use wildcard type in client code
2. Comparable and Comparators are comsumer. Eg: `Comparable<String>` consume a String and produce a integer. 
   => A properly design of generic should be `Comparable<? super T>` insead of `Comparable<T>`. Eg:  
``` java
	<T extends Comparable<? super T>> T max(List<? extends T> list); // 1

    <T extends Comparable<T>> max(List<? extends T> list) // 2
```
=> Method 1 will work for `ScheduledFuture` but 2 will not because it implement `Comparable<Delay>`, not `Comparable<ScheduledFuture>`.

