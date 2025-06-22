# Query lookup strategies

Spring support defining queries manually via string (Using named query method or `@Query`) or have them derived from method name (Derived query methods).

You could modify the query lookup strategy via `queryLookupStrategy` of `EnableJpaRepositories` annotation or via xml configuration.

There are 3 query lookup strategies:

- CREATE: Construct the query from method name
- USE_DECLARED_QUERY: find the declared query and throw exception if not found
- CREATE_IF_NOT_FOUND (default): combine CREATE and USE_DECLARED_QUERY 
