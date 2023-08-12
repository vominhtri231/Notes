# Configuration

Can be declare using `@Configuration` or `@SpringBootConfiguration` (which is just a alternative for `@Configuration`). Configuration can also be used to discover beans.

## Combine multiple configuration classes

The annotation `@Import` is used to combine multiple configuration classes

```java
@Configuration
@Import({ DogConfig.class, CatConfig.class })
class MammalConfiguration {
}
```

## Apply configurations

Adding the annotation `@EnableAutoConfiguration` to the class or declaring a class under the key `EnableAutoConfiguration` of `META-INF/spring.factories` to indicate a configuration as enable-auto. This allows the configuration to be applied.

**`@EnableAutoConfiguration` should only appear once**, there is no harm nor befifit from declaring multiple configuration with `@EnableAutoConfiguration`

The `@SpringBootApplication` already contain the `@EnableAutoConfiguration` so class that has the annotation is applied.

## Usage

Configuration is used to provide configuration or to:

### Discover beans

A configuration with `@ComponentScan` would help spring to find the wanted beans, by default it will look for beans in the current package and sub packages.

```java
@Configuration
@ComponentScan("a.b.c")
class Config {
    //...
}
```

The `@SpringBootApplication` already contain the `@ComponentScan` with default value. However, the annotation is still helpful when including third-party beans.


### Discover entities or repositories

To discover repository repos, we can use `@Enable...Repositories`, which can be `Jpa`, `Redis` repos, etc.
For entities, we can use `@EntityScan`.
Same with `@ComponentScan`, by default they will look for entities and repos in the current package and sub packages.

```java
@EntityScan(basePackages = {"com.sujan.example.entity"})
@EnableJpaRepositories(basePackages = "com.sujan.example.repository")
@Configuration
class Config {
   //...
}

```
