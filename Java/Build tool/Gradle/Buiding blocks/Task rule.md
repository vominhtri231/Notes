# Task rule

This technique allow specify logic base on the task naming pattern. A naming pattern include 2 parts: static potion and a placeholder.

Eg: the task `clean<TaskName>` is defined by Gradle for cleaning a task's outputs.

## Declare task rule

To create a task rule, you must get the TaskContainer under the `tasks` variable and using its `addRule(String, Closure)` method.

```groovy
tasks.addRule('Pattern: log<Task> .... ' , { taskName ->
  if(taskName.startWith("log")) {  // checking task name
     task(taskName) {  // dynamically create task
        // task declaration here
     }
  }
} 
```

## Note

* All task that is defined by task rule are grouped under `Rules` group and always be under that group
