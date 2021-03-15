1. JMS client
    * JMS sender (or JMS publisher, JMS producer)
    * JMS receiver (or JMS consumer, JMS subcriber)
2. Message Broker (or JMS Provider, JMS server)  
   The 3rd party system that responsible for implementing the JMS API.
3. JMS Message: contain data being transfered   
   Contains 3 parts:
    1. Header(required): data used to indentify and rounte message
    2. Properties: addition information for header
    3. Body: the actual data to be exchanged

A JMS provider must support 6 types of message:
1. Message: A message without message body
2. StreamMessage: Contains a stream of Java primitive types
3. MapMessage: Contains a set of name/value pairs
4. TextMessage: Contains a Java String
5. ObjectMessage: Contains a serialized Java object
6. BytesMessage: Contains a stream of bytes.

5. JMS Administered Objects: Configuring objects for the use of JMS client
    * Connection Factory: used to create connection between the application and the broker.
    * Destination: used to specify the destination of the sending message / source of the receiving message. There are 2 types of destinations correspondent to 2 message delivery models: Quece and Topic.

![](https://www.oracle.com/ocom/groups/public/@otn/documents/digitalasset/1577107.gif)
