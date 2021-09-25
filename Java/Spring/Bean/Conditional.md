# Conditional for creating beans

You could specify the condition for creating beans, it could be:

* Base on bean

```java
@Component
@ConditionalOnBean(value = RequiredBean.class)
public class AService {...}
```

* Base on class
* Base on properties

```java
@Component
@ConditionalOnProperty(name="a.property", havingValue="value",  matchIfMissing=true)
public class AService{...}
```

* Base on resource
