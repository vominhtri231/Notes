# Properties

Each instance of type like `Project` or `Task` provides property that can be accessed. If you want to declare extra properties, you could do it under the `ext` namespace.

```groovy
project.ext.a = 'a'

ext {
    b = 'b'
}
```

## Ways to declare properties

* Inside `build.gradle`
* In gradle.properties under `<USER-HOME>/.gradle` or project root
* Command-line options like `-D` or `-P`
* Environment property following the pattern `ORG_GRADLE_PROJECT_propertyX`
