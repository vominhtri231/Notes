## Intro
Entities could be mapped via mapping.xml or annotation.   
The entity class must obey Java Bean Standard which is a serializable class, has default constructor and setter & getter methods to initialize he attributes.

## Base annotation
| Annotation | Description |
| --- | --- |
| Entity | Declare the class as an Entity |
| Table | Declare the table name, its schema, its indexes, its unique constraints  |
| Id | Specify primary key of a table |

## Cascade operations
`DETACH`, `MERGE`, `PERSIST`, `REFRESH`, `REMOVE` , `ALL` (equivalent to cascade={DETACH, MERGE, PERSIST, REFRESH, REMOVE})

```java
@OneToMany(cascade=REMOVE, mappedBy="customer")
public Set<CustomerOrder> getOrders() { return orders; }