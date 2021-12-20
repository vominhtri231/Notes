# Dependency debug

## For display all dependencies of a project with their transitive dependencies and effective version

```sh
gradle dependencies
```

The result will be displayed from top to bottom

```txt
\--- org.jacoco:org.jacoco.ant:0.8.6
    +--- org.jacoco:org.jacoco.core:0.8.6
    |    +--- org.ow2.asm:asm:8.0.1
    |    +--- org.ow2.asm:asm-commons:8.0.1
    |    |    +--- org.ow2.asm:asm:8.0.1
    |    |    +--- org.ow2.asm:asm-tree:8.0.1
    |    |    |    \--- org.ow2.asm:asm:8.0.1
```

## For resolving version of a specific dependency and explaining why the version is chosen

```sh
gradle dependencyInsight --configuration <configuration> --dependency <dependency>
```

The result will be displayed from bottom to top

```txt
\--- com.a:abc:201.0.0-SNAPSHOT
    +--- compileClasspath
    \--- project :xyz
        +--- compileClasspath
        \--- com.a:def:201.0.0-SNAPSHOT 
```

## For detecting any version conflicts

```groovy
configurations.implementation.resolutionStrategy {
    failOnVersionConflict()
}
```
