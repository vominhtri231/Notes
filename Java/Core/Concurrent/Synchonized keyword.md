## How it works
The `synchronized` keyword is used to ensure that only one thread could execute a block of code at one time. 

```java
Object o = new Object();
synchronized (o) { // o is monitor object here
    ...
}
```
Java will block only if 2 or more threads invoke with the exact same monitor object.  

Synchronize on method is equivalent to using the object as monitor object, synchronize on static method is equivalent to using class as monitor object.

## Purposes
1. **Mutual exclusion**   
  Guarantee that object not be seen in an inconsistent state by one thread, while being modified by another.
2. **Communication between threads**  
  Without `synchronized`, changes in one thread may not be visible to others. Eg:
``` java
    private static boolean isStop;

    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(() -> {
            int i = 0;
            while (!isStop) i++;
        });
        thread.start();

        Thread.sleep(1000);
        isStop = true;
    }

```
In this example, the program  will never end because the change of `isStop` is un-noticed by the background thread.

## Remark  
1. To guarantee that synchronization is work, **both read and write operations** has to be synchronized.  
2. For communication purpose only, consider `volatile` keyword, which guarantees that read a variable will return most recently written value.
3. Prevent calling alien code inside synchronized block because it could lead to death-lock, reduce performance, exception, etc. 
   As a common rule, do as little as possible in synchronized block.

