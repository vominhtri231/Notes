### Intro
A JMS session is an object to maintain connection, a link between the connection and the thread handle it. It is a "single-thread context" so different threads must create different JMS sessions.

### Transacted Vs Acknowledged
* Acknowlegded:  After consumer __processed__ a message, it will send a ACK message to the producer. If not, the message will be redelivered. If the consumer start after a crash, it will receive all messages not been acknownleaded.  
  Their are different forms of acknowlegded:
    * Auto-acknowledge: the API will call acknowleged for you after the message returns sucessfully from the `receive` method call or `MessageListener` successfully returns.
    * Client-acknowledge: A client acknowledges a message by calling the method `acknowledge` of the message.
    * Dups-ok-acknowledge: Session lazily acknowledge the message. That could lead to possible message duplication => Reduce the work to prevent duplicates but should be used only by consumer tolerant of duplicate messages.
* Transacted: Group send or receive operations in a group on the session. All operations are known as success or fail at the time of commiting (all-or-nothing).
    * Pros: High gurantee and can group operations
    * Cons: Latency and performance
