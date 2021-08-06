# Spring retry

## Prequisition

For using spring retry, project must:
1. Include dependencies: 
`org.springframework.retry:spring-retry` as well as `org.springframework.spring-aspects`
2. Be configured with `@EnableRetry`

## @Retryable

Indicate method to be retried.

```java
@Retryable(
maxAttemptsExpression = 5,
backoff = @Backoff(delayExpression = 2000),     
include = RuntimeException.class
exclude = IOException.class)
void getName(){
    //...
}
```