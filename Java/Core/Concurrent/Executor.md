# Executor

 Using Executor instead of Thread to separate the tasks (Runnable/Callable) and the execution mechanism

## Using executor service

```java
ExecutorService executor= Executor.newSingleThreadExecutor();
executor.execute(()=>{
    // run the task
});
executor.shutdown();
```

### Trigger tasks

You could wait for all tasks by `#invokeAll(Collection<Callable>)`, wait for any of the task by `#invokeAny(Collection<Callable>)` or wait for a particular task by `Future#get()`

### Shutdown executor

Using `#shutdown`  to shutdown executor orderly submitted tasks, using `#shutdownNow` to stop executing tasks. These methods will not wait for the task to be stopped, using `#awaitTermination` to do that.

```java
service.shutdown()
if (!service.awaitTermination(10, TimeUnit.MINUTES)) {
  service.shutdownNow()
}
```

## Executor service's implementations

  1. Executors.newCachedThreadPool: no queue, create a new thread if no threads are available.
  2. Executors.newFixedThreadPool: using a fixed thread pool.
  3. ThreadPoolExecutor: For maximize control over the executor.'
  4. ScheduledThreadPoolExecutor: To schedule tasks to run at a particular time or to run periodically. 
     This is preferred than Timer/TimerTask because it is more versatile. 
     Config ScheduledThreadPoolExecutor with one thread makes it equivalent to Timer.
  5. ForkJohnPool: support fork join task. Fork join task allows splitting (fork) the task into subtasks and then combine them (join). 
     It's also using the work-stealing algorithm, make the task run very efficiently.  
     Parallel streams are written atop fork join pools.
