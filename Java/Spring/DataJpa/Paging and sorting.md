# Paging and sorting 

Using `PagingAndSortingRepository` for paging and sorting in spring data jpa.

```java
public interface ProductRepository extends PagingAndSortingRepository<Product, Integer> {

    List<Product> findAllByPrice(double price, Pageable pageable);
}
```

All you need to do is defining a `Pageable` object via:

* `Sort.by("name")`
* `PageRequest.of(1, 5)`
* `PageRequest.of(0, 5, Sort.by("price").descending().and(Sort.by("name")))`
