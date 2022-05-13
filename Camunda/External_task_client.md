# External task client

The camunda external task client allows user set up remote service tasks. There is support for Java (both plain Java and Spring) and Javascript implementations.

## How it communicates

![](./img/externalTaskCient.png)

The client allows to handle service tasks of type `external`.

It communicates with the Camunda Engine via HTTP . Users can add additional headers like basic authentications or custome interceptions.

Whenever an external service task is declaired, a topic name must be specify.
When the client subscribes to the topic, it fetches continueously for external tasks provided by the engine and marked it with a temporary lock so no other clients can work on it in the meanwhile.

```xml
<bpmn:serviceTask id="Activity_0vufnso" name="wait for all temp solutions being pushed" camunda:type="external" camunda:topic="checkWorkersFinished">
```

## Handler

Handler is used to implement custome methods which is executed everytime an external task is fetched and locked. For each subscription, a handler is required. In this handler, we could:

* Mark the task as be completed after the custom methods are completed  - then the execution can move on to the next task.
* Extend the lock duration when the custom methods take longer than expected.
* Unlock the task, so other client can fetch and lock this task again.
* Report failures if face an unsolvable problem

## Variable

Variables can be treated as process or local variables. Process variables available on all child scopes in the entire process. In the contract, the local variables availables available on the provided execution scope.

Saving variable does not gurantee that they are persisted. They only availabe at runtime and get lost if they are not shared by completing the external task.

Variables is saved as map and must be serializable.

```java
ExternalTaskService externalTaskService = ..;
ExternalTask externalTask = ..;

// get typed variable
JsonValue jsonCustomer = externalTask.getVariableTyped("customer");

// get non-types variable
Integer val1 = (Integer) execution.getVariable("val1");

// complete a task will persist variables
VariableMap variables = Variables.createVariables();
externalTaskService.complete(externalTask, variables);
```
