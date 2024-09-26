# Dependency configuration

Dependency configurations are scopes for dependencies, you could also think of them as a way to group dependencies with the same responsibility.

For example: `implementation` or `api` are dependency configuration.

## API

Configurations are managed by `ConfigurationContainer`, which can be access via `configurations` variable of `Project`.
The `ConfigurationContainer` allow you to add or get the `Configuration`s.

A `Configuration` has name, description, visibility and can be used to describe:

- resolution strategy (By default Gradle will simply choose the newer version). It could be accessed via `#resolutionStrategy(Closure)` method.
- include transitive dependencies or not
- extends from what configurations

## Add dependency configuration

Usually, it is added by applying plugins. E.G. Java plugin added configurations `implementation`, `testImplementation`, `api`, etc to project.  

You could create could own customize configuration. This can be handy if you need special group for the dependency, like included them in the built jar file (fat jar).

```groovy
configurations {
    extraLibs
}

dependencies {
    extraLibs "io.github.classgraph:classgraph:4.8.175"
}

task deploy() {
    // get dependencies of the configuration as file tree
    Configuration extraLibsConf =  configurations.extraLibs// Or configuration.getByName('cargo')
    FileTree deps = extraLibsConf.asFileTree  
}
```

```kotlin
val extraLibs: Configuration by configurations.creating

dependencies {
    extraLibs("io.github.classgraph:classgraph:4.8.175")
}

tasks.jar {
    from({
        extraLibs.map { if (it.isDirectory) it else zipTree(it) }
    })
}
```
