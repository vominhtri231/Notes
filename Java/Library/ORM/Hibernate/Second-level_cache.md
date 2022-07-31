# Second-level cache

## Introduction

Most ORM frameworks have the first-level cache, when the entities are loaded into persistent context. It is session-scoped, means once the session is closed, the cache is terminated. This is allow current session work with entity instances in isolation.

The second-level cache in Hibernate is SessionFactory-scoped, which is shared between sessions created by the same session factory.

This technich would help eliminate access cost to frequently access data, however it should only be used when read/write ratios of the cache content is high.

## Usage

To use second-level cache in Hibernate, we need to:

1. Specify the **cache provider** by provide an implementation of `org.hibernate.cache.spi.RegionFactory` (Eg hibernate-ehcache)
2. Provide these JPA properties:
  `hibernate.cache.use_second_level_cache=true`
  `hibernate.cache.region.factory_class=org.hibernate.cache.ehcache.EhCacheRegionFactory`
3. Add annotation `@org.hibernate.annotations.Cache` with the appropriate caching on the entity required concurrent caching strategy.

## Concurrent caching strategy

- `READ_ONLY`: For those entity that never change (exception is thrown when update happens)
- `NONSTRICT_READ_WRITE`: Only update cache when the update transaction is committed (User may face small time window of stale data)
- `READ_WRITE`: When the entity is updated, a soft lock is created on the second-level cache and released after transaction is committed.(strong consistency)
- `TRANSACTIONAL: A change is either committed or rolled back in both database and the cache.
