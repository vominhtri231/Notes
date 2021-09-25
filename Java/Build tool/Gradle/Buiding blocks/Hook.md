# Hook

Hooks can be used to execute code when specific event occurs. Eg: When project is loaded or build is fail, etc.

## You could create a hook via

* Closure

```groovy
gradle.projectsLoaded { gradle ->
 // Hook after project loaded
}

gradle.beforeProject { project ->
 // hook before project evaluation
} 

gradle.taskGraph.whenReady { graph ->
 // hook after task graph has been populated
}

gradle.buildFinished { result ->
  // hook after build finished
}
```

* Listener implementation

Advantages of listener implementation over closure is that you could reuse it and test it.
You have to create an implementation of the wanted hook and add it.

```groovy
class AListener implements TaskExecutionGraphListener { // the listener get called after the task graph has been populated
    @Override
    void graphPopulated(TaskExecutionGraph taskGraph) {
        ...
    }
}

gradle.taskGraph.addTaskExecutionGraphListener(new AListener())
```

## Init folder

The gradle init folder is located in `<USER_HOME>/.gradle/init.d`. Gradle would run any .gradle script inside this folder first.

=> This is the appropriate placed for putting the hook for those event when the project is getting created.
