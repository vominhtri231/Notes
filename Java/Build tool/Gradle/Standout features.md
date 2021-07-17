# Standout features

## Incremental build

Gradle would cache the build result and associate with input's hash value.  
If input is unchanged, the cache will be used. The task will be marked as UP-TO-DATE

## Wrapper

This allow to run the build script consistently, without cares for gradle version nor operating system.
Wrapper is consider as Gradle best practice and the wrapper files should be checked to the version control.

The wrapper files should be organized as below:

```java
task wrapper(type: Wrapper) { 
  gradleVersion = '1.7'  // task for generating wrapper files
}


|-build.gradle
|-gradle
|    |-wrapper
|       |-gradle-wrapper.jar // contain binary just for resolving gradle wrapper
|       |-gradle-wrapper.properties // contain properties for just resolving gradle wrapper like distribution URL
|-gradlew  // the file for executing gradle wrapper in UNIX
|-gradlew.bat  // the file for executing gradle wrapper in WINDOW
```

At the first run, the gradle will be downloaded and saved in `/user-home/.gradle/wrapper/dists`.
