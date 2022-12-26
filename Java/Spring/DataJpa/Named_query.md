## Named query

Named query can be declared:

- inside the entity class using `@NamedQuery` or `@NamedNativeQuery` 
- via the xml tag `<named-query>` or `<named-native-query>` in orm.xml JPA configuration file 

```java
@Entity
@NamedQuery(name = "User.findX", query = "select u from User where u.username = ?1")
public class User {

}
```

To use the named query define the method with the same name in the repository. By default, Spring Data would try to resolve it.

```java
public interface UserRepo extends JpaRepository<User, Long> {
  List<User> findX(String username)
}
```

For paging of native query, we need to specify another query with the suffix `.count` for the given named query

```java
@Entity
@NamedNativeQueries({
    @NamedNativeQuery(name = "User.findX", query = "select u from USERS where USER_NAME = ?1")m
    @NamedNativeQuery(name = "User.findX.count", query = "select count(*) from USERS where USER_NAME = ?1")
})
```
