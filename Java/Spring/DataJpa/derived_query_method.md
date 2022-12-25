# Derived query methods

Spring allow query creation via the method name

It can be applied for both find or delete/count/exist/update queries.

## Query lookup strategies

You could modify the query lookup strategy via `queryLookupStrategy` of `EnableRepositories` annotation or via xml configruration

There are 3 query lookup strategies:

- CREATE: Construct the query from method name
- USE_DECLARED_QUERY: find the declared query and throw exception if not found
- CREATE_IF_NOT_FOUND: combne CREATE and USE_DECLARED_QUERY (default)

## Filter conditions

The mechinism would strip the prefixes `find..By`, `delete..By`, `get..By`, etc from the method name and parse the criterias from it.

```java
List<User> findByUsername(String username);
```

By default the filter comparation is `equals`.
For more complex comparation like not equals, greater, less than, after, before or string relative comparation, etc consulting the [docs](https://docs.spring.io/spring-data/jpa/docs/1.8.x/reference/html/#jpa.query-methods.query-creation)

## Nested property paths

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

To sorting or limiting dynamically, we could use `Pagable` or `Sort` keyword on `PagingAndSortingRepository`
In a `Pagable` already contains the sort option, so only use the `Sort` if you only need dynamic sorting.

The return collection can be a `Page` or `Slice`.
A `Page` contains the imformation about total number of elements and pages available. 
This also cost an additional count query execution.
A `Slice` only knows whether there's a next slice avalable, which can be appropriate for a large data set.

```java
List<User> findByUsername(String username, Pagable pageble)

Page<User> findByUsername(String, Pagable pageble)

Slice<User> findByUsername(String, Pagable pageble)
```

## Alternatives

Instead of derived query method, which could produce a long and hard to read method name, we could use named query instead

```java
@Entity
@NamedQuery(name = "User.findX", query = "select u from User where u.username = ?1")
public class User {

}

List<User> findX(String username)
```

For a large nubmer of queries, we could use `@Query` instead. 
Using `@Query`, we could using native sql instead of hql, which can be required for complex sql queries.
Also, we could using named parameter `@Param` instead of parameter position to prevent errors.

```java

@Query('select u from User u where u.username = ?1')
List<User> findX(String username)

@Query('select * from USERS where USER_NAME = ?0', nativeQuery = true)
List<User> findX(String username)

@Query('select u from User u where u.username = :username')
List<User> findX(@Param("username") String username)
```
