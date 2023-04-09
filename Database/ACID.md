# ACID

## What is ACID ?

ACID describes properties of transactions:

* A - Atomicity: Transaction execute as a unit - all or nothing executed
* C - Consistency: Constraints must be maintained
* I - Isolation: Transactions don't know about each other
* D - Durability: Changes of transaction should be durable

## Level of isolation:

There are multiple isolation problem can happen:

* Lost update
* Uncommited read
* Unrepeatable read
* Phantom read

For absolute isolation, the cost for performance and scalability can be too high, so ANSI's specification can allow multiple level of isolations, list in increase level of isolation:

* Read uncommited:  
  Prevent lost update but not uncommited read by using a write lock. A write transaction block other write transactions, so other write transaction will not lost update but read transactions can still read the uncommitted data  
  => This level of isolation should be avoided, since the unwanted data from a rollbacked transaction can be persistedss
* Read commited
  Prevent uncommited read but not unrepeatable read by using a shared read lock and multiple write locks. A write transaction will block other read transactions as well as write transactions, so read transactions can not read uncommited data.  
  => Eventhough unrepeatable read can happen, this level of isolation is quite balance between performace and correctness, especially if we combine with application locks (optimistic or pesimistic locks). Many verdor using this level of isolation as default.
* Read repeadable  
  Prevent unreapeadable read but not phantom read. A read transaction will block the write transaction but not other read transaction, write transaction will block all transactions.
* Serialized  
  When a write transaction executed on a table/ resource, other transaction can not touch it
  => Need to be avoided, as performance may suffer.
  