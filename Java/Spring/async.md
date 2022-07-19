# Async

`@Async` supports asynchronous execution in Spring. Annotate a method of a bean with `@Async` would make it executed in a separate thread.

## Configuration

To enable async support

```java
@Configuration
@EnableAsync
public class SpringAsyncConfig { ... }
```

## Limitations

`@Async` has 2 main limitations:

- Must be applied in public method
- Self-invocation can not work. This can be solved by declaring an instance of the bean
  
## Executor

By default, `@Async` would use `SimpleAsyncTaskExecutor`, to change the executor implementation, you could either:

- Override the `AsyncConfigurer` - this would apply the change to the whole application
- Provide the execution bean name at the `@Async`

```java
@Bean(name = "aExecutor")
public Executor aExecutor() {
    ...
}

@Async("aExecutor")
public void abc(){
    ...
}
```

## Exception handling

```java
public class CustomAsyncExceptionHandler implements AsyncUncaughtExceptionHandler {

    @Override
    public void handleUncaughtException(Throwable throwable, Method method, Object... obj) {
       // ...
    }
    
}
```
