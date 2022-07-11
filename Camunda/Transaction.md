# Transaction

When there is an external trigger, the engine will run until it encounter a wait state, 
then it will persist the current execution and wait to be triggered again.
Here, wait states act as transaction boundaries.

## Wait state

A wait state is a task that is executed later, including: User task, receiving task, message event, timer event,
event based gateway, external task service, etc.

## Asynchronous Continuations

For other services except for external task service, Asynchronous Continuations can add additional transaction boundaries.

They can be added via tag `camunda:asyncBefore` and `camunda:asyncAfter`.
