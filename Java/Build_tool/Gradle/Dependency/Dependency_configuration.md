# Dependency configuration

Dependency configurations are scopes for dependencies, you could also think of them as a way to group dependencies with the same responsibility.

## API

Configurations are managed by `ConfigurationContainer`, which can be access via `configurations` variable of `Project`.
The `ConfigurationContainer` allow you to add or get the `Configuration`s.

A `Configuration` has name, description, visibility and can be used to describe:

- resolution strategy (By default gradle will simply choose the newer version). It could be accessed via `#resolutionStrategy(Closure)` method.
- include transitive dependencies or not
- extends from what configurations

## Add configuration

Usually, it is added by applying plugins. Eg: Java plugin added configurations `implementation`, `testImplementation`, etc to project.  
You could create could own customize configuration.

```groovy
configurations {
    cargo {
        description: 'Deploy dependency configuration'
        visibility: false
    }
}

task deploy() {
    Configuration cargoCon =  configurations.cargo // Or configuration.getByName('cargo')
    FileTree deps = cargoCon.asFileTree // get dependencies of the configuration as file tree 
    ...
}
```
