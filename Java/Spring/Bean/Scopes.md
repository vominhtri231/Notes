# Bean scopes

The bean scope define the lifecycle and visibility of the bean

## Singleton scope

Container create a single instance of that bean and return it every time it get requested (default scope).

## Prototype scope

Container return a different instance every time it get requested

```java
@Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)
@Component
class AController {
    ...
}
```

## Web aware scopes

There are 4 additional scopes that only available in web-aware application context.

1. Request scope
2. Session scope
3. Application scope
4. WebSocket scope
