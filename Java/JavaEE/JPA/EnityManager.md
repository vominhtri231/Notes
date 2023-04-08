# Entity Manager

Persistence context is a cache of entity instances (the first level cache - which is can not be turned off).
It remember all modifications and state changes made in a unit of work, enable dirty checking.
So if the wanted object is already in the persistent context (loaded before) or no changes are made to the saving entity, no query will hit the DB at all.

Entity manager is used to manage the entities in the persistence context. Each entity manager is associated with a persistent context. `EntityManager` defines methods to interact with the persistent context.  

One the unit of work is done, all the modifications can be persisted, 
or we can explicitly do that by calling `EntityManger#flush`.
JPA providers usually would try to delay synchronizing changes to the DB as long as possible to enhance performance and prevent locks.

In JPA terms, there are 2 types of entity manager:

## Container-Managed Entity Manager

The entity manager's persistent context is automatically propagated by the Java EE container to all application components. The Java EE container will also manage the lifecycle of entity managers as well as the transaction (e.g. using `@javax.transaction.Transactional`)

```java
@PersistenceContext(unitName = "persistent-unit")
EntityManager em;
```

## Application-Managed Entity Manager

The persistence context is not propagated automatically, each time an entity manager is created , it will create a new, isolated persistent context.

```java
// Create entity manager factory
EntityManagerFactory emFactory = Persistence.createEntityManagerFactory("persistent-unit");
// or 
@PersistenceUnit
EntityManagerFactory emFactory;

// This also create the persistent context
EntityManager entityManager = emFactory.createEntityManager();

// For resource local transaction
EntityTransaction transaction = entityManager.getTransaction();

transaction.begin();
// the unit of work
transaction.commit();
// the object changes will be auto migrated at this point
```
