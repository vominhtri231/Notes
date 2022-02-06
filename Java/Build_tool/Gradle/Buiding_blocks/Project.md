# Project

Each project represent a thing you're trying to build or achieve. A project can be used to declare tasks, dependencies, configuration, etc; apply plugins, etc.

Each Gradle build script must declare at least one project. Gradle also support for multiple projects builds.

## `project` instance

Gradle will based on your configuration on build.gradle to create a variable named `project` of type `org.gradle.api.Project`. (It is optional to use `project` instance to access the project's properties and methods)

```groovy
setDescription("abc")
println "$project.description"
println "$description"
```
