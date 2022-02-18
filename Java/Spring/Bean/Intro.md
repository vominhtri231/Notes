# Bean

Spring beans are objects that are managed by Spring IoC container.
You could declare an object as bean via `@Component` for class or `@Bean` for method.

## Recognition

Spring uses `@ComponentScan` to configure where to look for beans, by default it will look for beans in the current package and sub packages.

```java
@Configuration
@ComponentScan("a.b.c")
class Config {
    ...
}

```

The `@SpringBootApplication` already contain the `@ComponentScan` with default value. However, the annotation is still helpful when creating third-party beans.
