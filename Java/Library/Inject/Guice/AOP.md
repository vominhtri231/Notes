### Intro
Guice supports method interception, allows you to write code excecuted each time a matching method is invoked. It's suited for cross cutting concerns (aspects), such as transactions, security, logging, etc.

Guice using this techniche to design `@Transactional` which will open the transaction before the invocation and will commit/rollback after the invocation.

### Components
1. Matcher  
   A simple interface that define the acceptance senerior for classes/methods. It could be annotated with, in package, in subpackage, subclass, etc. There is a factory class for it.
2. MethodInterceptor  
   It is executed whenever a matching method is invoked. They may inspect the method, its arguments, return value, exception, etc.

### Example
Forbid a method calls in the weekend

```java
@Retention(RetentionPolicy.RUNTIME) @Target(ElementType.METHOD)
@interface NotOnWeekends {}
```

```java
public class RealBillingService implements BillingService {

  @NotOnWeekends
  public Receipt chargeOrder(PizzaOrder order, CreditCard creditCard) {
    ...
  }
}
```

```java
public class WeekendBlocker implements MethodInterceptor {
  public Object invoke(MethodInvocation invocation) throws Throwable {
    Calendar today = new GregorianCalendar();
    if (today.getDisplayName(DAY_OF_WEEK, LONG, ENGLISH).startsWith("S")) {
      throw new IllegalStateException(
          invocation.getMethod().getName() + " not allowed on weekends!");
    }
    return invocation.proceed();
  }
}
```

```java
public class NotOnWeekendsModule extends AbstractModule {
  protected void configure() {
    bindInterceptor(Matchers.any(), Matchers.annotatedWith(NotOnWeekends.class),
        new WeekendBlocker());
  }
}
```

[Source](https://github.com/google/guice/wiki/AOP)