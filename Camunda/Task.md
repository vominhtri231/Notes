# Task

A camunda task can be configured in multiple ways:

## Script task

Using script for handling tasks, which can be JS, groovy, JRuby, Jython scripts.

```groovy
inputArray = execution.getVariable('inputArray')
sum = 0

for ( i in inputArray ) {
    sum += i
}

execution.setVariable('sum', sum)
```

## Internal service task

Using the classes/services deployed along with the process application for handling tasks.
They can be declared as:

* Java class that extends `JavaDelegate` class
```xml
<seviceTask 
    id="javaService"
    name="My Java Service Task"
    camunda:class="org.camunda.bpm.MyJavaDelegate" />
```
* Expression of a java command
```xml
<serviceTask 
    id="aMethodExpressionServiceTask"
    name="My Expression Service Task"
    camunda:expression="#{myService.doSomething()}"/>
```

## External service task

Using external services for handling tasks.
Camunda provide a set of task client APKs for writing those external services in python, java, etc.
A service task would be defined using `external` type and a topic. Those external services would subscribe into that topic.
After a task is created, the process application would pull the subcribed services and call them.

```xml
<serviceTask 
  id="validateAddressTask"
  name="Validate Address"
  camunda:type="external"
  camunda:topic="AddressValidation" />
```
