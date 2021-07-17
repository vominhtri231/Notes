# Entity Manager
Persistence context is a cache of entity instances. Entity manager is used to manage the entities. Each entity manager is associated with a persistent context - a set of managed entity instances. `EntityManager` defines methods to interact with the persistent context.  
There are 2 types of entity manager:
## Container-Managed Entity Manager
The entity manager's persistent context is automatically propagated by the Java EE container to all application components. The Java EE container will also manage the lifecycle of entity managers as well as the transaction (e.g. using `@javax.transaction.Transactional`)

```java
@PersistenceContext(unitName = "persistent-unit")
EntityManager em;
```
## Application-Managed Entity Manager
The persistence context is not propagated automatically (each entity manager will create a new, isolated persistent context) and the lifecycle of entity managers and the transaction are managed by the application itself.

**NOTE:**
* Container managed entity manager cannot be used if the transaction type is RESOUCE_LOCAL.
* TOMCAT does not support JTA transaction out of the box, you could use standalone transaction manager such as Atomikos, JOTM, Bitronix, SimpleJTA, etc.

```java
// Create entity manager factory
EntityManagerFactory emFactory = Persistence.createEntityManagerFactory("persistent-unit");
// or 
@PersistenceUnit
EntityManagerFactory emFactory;

EntityManager entitymanager = emFactory.createEntityManager();

// To gain access to the transaction
// For JTA transaction
@Resource
UserTransaction transaction;
// For resource local transaction
EntityTransaction transaction = entityManager.getTransaction();


transaction.begin();
// Work with the persistence context ...
transaction.commit();
// the object changes will be auto migrated at this point
```

# Entity states
![](https://cdn.jstobigdata.com/wp-content/uploads/2019/08/Entity-instance-states.png)

1. New (Transition) state  
   An object is newly created and never been associated with Persistent context(Hibernate session) is in the New state.
2. Persistent (JPA managed) state  
   An object is associated with persistent context is in Persistent state.  
   Any changes made toward objects in this state are automatically propagated to databases.
3. Detached (unmanaged) state  
   An object is becomes detached once the currently running session is closed.  
   To synchronize the changes of detached or new object, using `merge`.
4. Removed state  
   Associated with the persistent context but are scheduled for removal from the data store.
