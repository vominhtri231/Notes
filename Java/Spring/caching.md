# Spring cache

## Dependencies

In spring, there is the package `spring-context` that provides cache functionality.

There is also the package `spring-context-support` that provides cache manager implementations backed by `EhCache` or `Caffein`. 
It also includes `spring-context`.

For spring-boot users, there is the dependency `spring-boot-starter-cache` that use `spring-context-support` under the hook.
It would also use the `ConcurrentMapCacheManager` by default as the cache manager.

## Configuration

### Enable caching

To enable caching, adding `@EnableCaching` annotation in the configuration class and declare a bean of type `CacheManager` (no need if you are using spring-boot)

```java
@Configuration
@EnableCaching
public class CacheConfig {
  // TO DO
}
```

## Declare caching

To cache a method, adding the `@Cacheable` annotation in the method, using it on the class level for caching every methods of the class.
You need to specify the cache name for where to save the cache.
By default, the key for saving the cache is generate by hasing the given parameters or returning the parameter if there is only one.
You could specify the key function using SpEL or the key generator.

```java
@Cacheable("address")
public String getAddress(Employee employee){
  // TO DO
}
```

## Invalidate cache

To invalidate cache, using the annotaion `@CacheEvict` for the method that remove the cache and `@CachePut` for the method that update the cache.
The key for cache item must be the same for the invalidation to be effective.

```java
@CacheEvict("address")
public String deleteAddress(Employee employee){
  // TO DO
}

@CachePut("address")
public String updateAddress(Employee employee){
  // TO DO
}
```
