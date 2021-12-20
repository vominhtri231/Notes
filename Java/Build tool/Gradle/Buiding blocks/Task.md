# Tasks

Each task's declaration will be used to create an instance of type `org.gradle.api.Task`.

By default with the task would have type `DefaultTask`. To specify the task type: `task abc(type: Zip) {}`. Gradle provides a broad spectrum of predefined tasks. You could also write your own custom task.

## Configurations

They are configured inside the task block and will be executed any task actions - should be used to setting up configuration required for projects/tasks.

Keep in mind that configuration is executed for every build, even if with `gradle tasks`.

```groovy
task abc {
  println "Configuration phase"
}
```

## Actions

An action is the place for the build logic, which can be add by `doFirst(Closure)` and `doLast(Closure)` methods. Internally, each task has a list of task action and execute it sequentially. You could use this mechanism for adding custom logic of task you didn't write.

```groovy
task abc {
    doFirst {
        println "Before"
    }

    doLast {
        println "After"
    }
}
abc.doFirst { println "First action" } // add the action to the beginning of the list
abc.doLast { println "Last action" } // add the action to the end of the list
```

## Depends on

Declare task's dependencies by:

* methods `dependsOn` (explicit)
* declare a task's input as another task's output (implicit)

Note that this only defined the task's dependencies, not execute order of those dependencies.

## Finalizer

Declare task's finalizers as **clean up** tasks by method `finalizedBy`

## Input and output

Task's input could be file(s), a directory or a property. Task's output could be file(s) or a directory. They are used in incremental build (if input and output are not changed, the task will be skipped).  
As an alternative, you could implement the method `upToDateWhen(Closure)` which is evaluated at execution time instead of configuration time.

```groovy
task abc() {
    inputs.property('a', ext.a)
    outputs.file xyz

    doLast {
      // the actual build logic here ...
    }
}
```
