## Wait/notify
Standard idiom for using wait/notify:

```java
synchronized(obj) {
    while(<condition not hold the lock>){
        object.wait()
    }
}
```
=> Always use the wait loop  

## CountDownLatch

CountDownLatch's constructor takes an integer, indicates number of time the method countDown must be called before any all threads locked by it could run.

``` java
CountDownLatch run = new CountDownLatch(1);

executor.run(() -> {
    run.await(); // this will wait for run.countDown()
});

run.countDown();
```

## CycleBarrier

CycleBarrier's constructor takes an integer indicate number of thread must be waiting so every thread could continue to run.

``` java 
CycleBarrier run = new CycleBarrier(2);

executor.run(() -> {
    run.await(); // this will util both thread is waiting
});

run.await();
```

## Exchanger

Allow exchanging object between threads.

```java
Exchanger<String> exchanger = new Exchanger<>();


new Thread() {
    String exchangedString = exchanger.exchange("A")
}.start();

new Thread() {
    String exchangedString = exchanger.exchange("B")
}.start();
```

## Semaphore - Mutex

Using to restrict number of threads can access the resource.

```java
Semaphore semaphore = new Semaphore(4); //Maximum 4 threads can access the resource

semaphore.acquire();
try{
    // Doing the task ...
} finally {
    semaphore.release();
}

```

#### Note
* Mutex is the Semaphore that restrict one thread can access the resource.

