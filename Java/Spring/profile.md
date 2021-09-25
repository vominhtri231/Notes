# Profile

Any component can be specify for a profile

```java
@Configuration
@Profile("production")
public class ProductionConfiguration {

    // ...
}
```

## Active profiles

* The config `spring.profiles.active` or environment parameter `SPRING_PROFILES_ACTIVE` can be used to **replace** the active profiles.

* The config `spring.profiles.include` can be used to **add** to the active profiles.
