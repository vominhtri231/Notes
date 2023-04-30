# Mapping entities

Entities could be mapped via mapping.xml or annotations.  
The entity class must obey Java Bean Standard:

* is a serializable class
* has default constructor
* has setter & getter methods to initialize attributes.

## Basic annotations

| Annotation | Description |
| --- | --- |
| Entity | Declare the class as an Entity |
| Table | Declare the table name, its schema, its indexes, its unique constraints  |
| Id | Specify primary key of a table |

## Cascade operations

When the parent entity performs some actions, cascade options specify whether the associate entities will perform the same action or not.  
Cascade options are: `DETACH`, `MERGE`, `PERSIST`, `REFRESH`, `REMOVE` , `ALL` (propagate all actions)

```java
@OneToMany(cascade={REMOVE, PERSIST}, mappedBy="customer")
public Set<CustomerOrder> getOrders() { return orders; }
```

## hashCode() and equals()

### When

As the JPA specification, you need to implement the equals() and hashCode() for:

* Composite primary key
* one-to-many and many-to-many associations using collection type like Set or Map

### How

* When declaring hashCode() and equals() for entities, it is advised to prefer business key or natural key over generated key.
(The entity should be unique by these attributes).  
* The hash code of entities is not allow to change after added to Set or Map - so consider returning a fixed value if using generated key.  

## Multiple attributes primary key

```java

@Embeddable
class AKey implement Serializable {
    ... 
    // must implement hashCode() and equals() for every fields
}

@Entity
class AEntity {

    @EmbeddedId
    private AKey id;

    ... 
}

```
