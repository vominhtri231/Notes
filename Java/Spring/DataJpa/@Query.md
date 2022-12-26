# @Query

For a large nubmer of queries, we could use `@Query` instead of named query.
The `@Query` method would take precedence over the named query.

```java
@Query('select u from User u where u.username = ?1')
List<User> findX(String username)
```

Using `@Query`, we could using native sql instead of JPA query language, which can be required for complex sql queries, via `nativeQuery` tag.
For paging of native queries, you would need to specify the count query for it. Also, dynamic sorting is not available for native query.

```java
@Query(value = 'select * from USERS where USER_NAME = ?1', nativeQuery = true)
List<User> findX(String username)

@Query(value = 'select * from USERS where USER_NAME = ?1', 
       countQuery = 'select count(*) from USERS where USER_NAME = ?1',
       nativeQuery = true)
Page<User> findY(String username, Pageable pageable)
```

We could using named parameter `@Param` instead of position-based binding to prevent errors.

```java
@Query('select u from User u where u.username = :username')
List<User> findX(@Param("username") String username)
```
