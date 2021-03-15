## Introduction
 Using Executor instead of Thread to seperate the tasks (Runnable/Callable) and the execution mechanism
## Using executor service
```java
ExecutorService executorService = Executor.newSingleThreadExecutor();
exucutor.execute(()=>{
    // run the task
});
executor.shutdown();
```
* You could wait for all tasks by `#invokeAll(Collection<Callable>)`, wait for any of the task by `#invokeAny(Collection<Callable>)` or wait for a particular task by `Future#get()`.
* Using `#shutdown`  to shutdown excecutor orderly submitted tasks, using `#shutdowNow` to stop executing tasks. These methods will not wait for the task to be stopped, using `#awaitTermination` to do that.

## Executor service's implementations
  1. Executors.newCachedThreadPool: no queue, create new thread if no threads are available.
  2. Executors.newFixedThreadPool: using a fixed thread pool.
  3. ThreadPoolExecutor: For maximine control over the executor.'
  4. ScheduledThreadPoolExecutor: To schedule tasks to run at a particular time or to run periodically. This is preferred than Timer/TimerTask because it more versatile. Config ScheduledThreadPoolExcutor with one thread makes it equivilent to Timer.
  5. ForkJohnPool: support fork join task. Fork join task allows to split (fork) the task into subtasks and  then combine them (join). It also using the work-stealing algorithm, make the task run very efficiently. Parallel streams are written atop fork join pools.
