# JMS session

A JMS session is an object to maintain connection, a link between the connection and the thread handle it. It is a "single-thread context" so different threads must create different JMS sessions.

## Transacted Vs Acknowledged

* Acknowledged:  After consumer __processed__ a message, it will send a ACK message to the producer. 
  If not, the message will be redelivered. If the consumer start after a crash, it will receive all messages not been acknowledged.  
  There are different forms of acknowledged:
  * Auto-acknowledge: the API will call acknowledged for you after the message returns successfully from the `receive` method call or `MessageListener` successfully returns.
  * Client-acknowledge: A client acknowledges a message by calling the method `acknowledge` of the message.
  * Dups-ok-acknowledge: Session lazily acknowledge the message.  
  That could lead to possible message duplication => Reduce the work to prevent duplicates but should be used only by consumer tolerant of duplicate messages.
* Transacted: Group send or receive operations in a group on the session. All operations are known as success or fail at the time of committing (all-or-nothing).
  * Pros: High guarantee and can group operations
  * Cons: Latency and performance
