![](https://i.stack.imgur.com/B6H90.png)

### Point-to-point
A message created by a producer, pass to a queuce then delivered to one of the consumers registered for the queue.  
Each message is gurantee to be consume by one and only one consumer. If there are no consumers register, the message will be holden in the quece until it is deliverd.

### Publish-and-subscribe
A message created by a producer, pass to a topic then deliverd to all active subcriber to the topic.
Each message can be sent to any number of consumer. If there are no subscribers, the message will not be holden unless the topic has durable subscriptions for inactive subscriber.
Durable subscription represent a consumer registers for the topic, can be inactive at anytime, but gurantee to receive the message.
