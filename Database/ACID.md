# ACID

## What is ACID ?

ACID describes properties of transactions:

* A - Atomicity: Transaction execute as a unit - all or nothing executed
* C - Consistency: Constraints must be maintained
* I - Isolation: Transactions don't know about each other
* D - Durability: Changes of transaction should be durable

## Level of isolation:

There are multiple isolation problems can happen:

* Lost update
* Uncommitted read
* Unrepeatable read: In a transaction, a row is retrieved multiple time and the values differ each time.
* Phantom read: In a transaction, a query is executed multiple time and  and the returned rows are differ each time.

For absolute isolation, the cost for performance and scalability can be too high, so ANSI's specification can allow multiple level of isolations, list in increase level of isolation:

* Read uncommitted
  Prevent lost update but not uncommitted read by using a write lock. A write transaction block other write transactions, so other write transaction will not lost update but read transactions can still read the uncommitted data  
  => This level of isolation should be avoided, since the unwanted data from a rollbacked transaction can be persisted
* Read committed
  Prevent uncommitted read but not unrepeatable read by using a shared read lock and multiple write locks. A write transaction will block other read transactions as well as write transactions, so read transactions can not read uncommitted data.  
  => Even though unrepeatable read can happen, this level of isolation is quite balance between performance and correctness, especially if we combine with application locks (optimistic or pessimistic locks). Many vendor using this level of isolation as default like SQL server, Oracle, etc.
* Read repeatable
  Prevent unrepeatable read but not phantom read. A read transaction will block the write transaction but not other read transaction, write transaction will block all transactions. MYSQL uses this as the default isolation level.
* Serialized
  When a write transaction executed on a table/ resource, other transaction can not touch it
  => Need to be avoided, as performance may suffer.