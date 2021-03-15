## Intro
The techniche that allow you to have more than one instance of a dependent type or to lazily load an instance.

```java
public interface Provider<T> {
  T get();
}
```


## How to

To declare a provider:
```java
// In binding module
// The parameter(s) will be injected
@Provides
private User createUser(final UserRepo userRepo) {
    return userRepo.createUser();
}
```

Or
```java
class UserProvider implement Provider<User> {
    @Inject
    UserRepo userRepo;
    
    User get() {
        return userRepo.createUser();
    }
}

// In binding module
bind(User.class).toProvider(UserProvider.class);
```


In calling side:
```java
@Inject
Provider<User> userProvider;

User user = userProvider.get();
```