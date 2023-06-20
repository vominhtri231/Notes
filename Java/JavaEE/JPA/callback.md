# JPA callback
 
JPA allows us to listen to entities's events via callback methods.

## How to declare one

### Entity listener

We could either create an entity listener, then add to the entity we want to intercept.

```java

// The entity listener
// Entity listener must be stateless, the JPA engine automatically creates and destroys it. It also need to have a public no-args constructor.
public class NotifyEntityListerner {

  @PostPersist
  public void notify(Object entity) {

  }
}

// The entity we want to intercept
// @EntityListener accepts a list of entity listeners, which will be excecuted in order
@Entity
@EntityListerners(NotifyEntityListerner.class)
public class Item {

}
```

### Callback methods in entity class.

Or we can create a callback method directly in the entity class, with the parameter becomes `this` instance now. We can also declare the callback method in the parent entity class and it will be applied to all child entity classes. If multiple callbacks of the same type exists in the entity hirachy, the more generic one will be called first. 

```java
@Entity
public class User {

  @PostPersist
  public void notify {

  }
}
```

## Callback annotations 

There are some supported annotations for callback methods:

Annotation | When it is called |
-- | -- |
@PostLoad | Item is loaded into context or get refreshed
@PrePersist | `#persist` method or `#merge` method for trasient entity is called
@PostPersist |  After database operation is executed
@PostUpdate, @PreUpdate | Only when entity state is dirty
@PostRemoved, @PreRemoved | Entity is deleted
