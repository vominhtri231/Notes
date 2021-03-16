![](https://i.stack.imgur.com/B6H90.png)

### Point-to-point
A message created by a producer, pass to a queue then delivered to one of the consumers registered for the queue.  
Each message is guarantee to be consumed by one and only one consumer. 
If there are no consumers register, the message will be holden in the queue until it is delivered.

### Publish-and-subscribe
A message created by a producer, pass to a topic then delivered to all active subscriber to the topic.
Each message can be sent to any number of consumer. If there are no subscribers, 
the message will not be holden unless the topic has durable subscriptions for inactive subscribers.
Durable subscription represent a consumer registers for the topic, can be inactive at anytime, but guarantee to receive the message.
