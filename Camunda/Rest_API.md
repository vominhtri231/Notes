# Camunda Rest API

Camunda Rest API is built ontop of engine Java API => most of the task that available on Java API can do through the rest API. User can access all rest API document via swagger at `<camunda-url>/swaggerui`.

There are some well known entity types:

* Process's definitions: processes
    * POST `/process-definition/{id}/start`: start the given process
    * GET `/process-definition`: get processes via name, key, etc
* Process's instances: running process's instances
    * GET `/process-instance`: get process's instances via definition, variables, etc
* Task: user's tasks
    * GET `/task`: get user's tasks via instance id, task id, etc
    * POST `/task/{id}/complete`: completing user's task
