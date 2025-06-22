# Derived query methods

Spring allow query creation via the method name

It can be applied for both find or delete/count/exist/update queries.

Spring Data would strip the prefixes `find..By`, `delete..By`, `get..By`, etc from the method name and parse the criterias from it.

```java
List<User> findByUsername(String username);
```

By default the filter comparation is `equals`.
For more complex comparation like not equals, greater, less than, after, before or string related comparation, etc consulting the [docs](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation)

## Nested property path

For access the nested property path, we could use the underscore `_`

```java
List<User> findByName_FirstName(String firstName);
```

## Sorting and limiting

We could sort or limiting the query via the method name, using `OrderBy`, `Top` or `First` keyword

```java
List<User> findByUsernameOrderByAgeDesc(String username);

List<User> findFirstByOrderByAge()

List<User> findTop3ByNameOrderByAge(String username)
```

## Applied entity graph

To use the entity graph:

```java
@Repository
public interface GroupRepository extends CrudRepository<GroupInfo, String> {

  // With the predefined entity graph `GroupInfo.withMember`
  @EntityGraph(value = "GroupInfo.withMember", type = EntityGraphType.LOAD)
  GroupInfo getByGroupName(String name);

  // Without the predefied entity graph
  @EntityGraph(attributePaths = {"members"})
  GroupInfo getByName(String name)
}
```
