# Sorting and paging

For sorting and paging, we could use `PagingAndSortingRepository`, which support `Pagable` or `Sort` as additional parameters.

## Sorting

We could use `Sort` or typed safe `TypeSort`

```java
Sort sortA = Sort.by("name").ascending()
  .and(Sort.by("age").descending);

TypeSort<User> userSort = Sort.sort(User.class)
Sort sortB = userSort.by(Person::getName).ascending()
  .and(userSort.by(Person::getAge).descending())
```

To use the `Sort` parameter

```java
List<User> findByUsername(String username, Sort pageble)
```

## Paging

The return collection can be a `Page` or `Slice` for paging query methods.
A `Page` contains the imformation about total number of elements and pages available. 
This also cost an additional count query execution.
A `Slice` only knows whether there's a next slice avalable, which can be appropriate for a large data set.

```java
List<User> findByUsername(String username, Pagable pageble)

Page<User> findByUsername(String, Pagable pageble)

Slice<User> findByUsername(String, Pagable pageble)
```
