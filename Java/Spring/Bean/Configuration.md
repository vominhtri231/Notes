# Configuration

A bean that provide configuration.

## Import

The annotation `@Import` is used to combine multiple configuration classes

```java
@Configuration
@Import({ DogConfig.class, CatConfig.class })
class MammalConfiguration {
}
```

## Auto configuration

Adding the annotation `@EnableAutoConfiguration` to the class or declaring a class under the key `EnableAutoConfiguration` of `META-INF/spring.factories` to indicate a configuration as enable-auto. This allows the configuration to be applied.

The `@SpringBootApplication` already contain the `@EnableAutoConfiguration` so class that has the annotation is applied.
