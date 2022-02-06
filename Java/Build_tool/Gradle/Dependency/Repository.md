# Repository

## API

Repositories in gradle is managed by `RepositoryHandler`, which can be managed via variable `repositories`. You could declare multiple repositories, and will be used based on the declaring order.

Gradle support various type of repository, including:

## Maven repository

Maven repository map the artifact by creating directories for each group levels and version. It will also saved both binary and the metadata in the same folder.

Gradle support some predefined maven repo, including `mavenLocal()`, `mavenCentral()`. You could also add your own repo via `maven` or `mavenRepo` methods.

```groovy
repositories {
    maven {
        name 'abc'
        url 'http://repo-abc'
    }
}
```

## Ivy repository

Instead of fixed layout like maven, Ivy has customized layouts.

```groovy
repositories {
    ivy {
        url 'http://repo-abc'
        layout 'patter', {
            artifact '[organization]/[module]/[revision]/[artifact]-[revision].[ext]' // layout for artifact
            ivy '[organization]/[module]/[revision]/ivy-[revision].xml' // layout for metadata
        }
    }
}
```

## Flat directory repository

The directory containing artifacts, without any metadata(s) => you must manage transitive dependencies by your own

```groovy
repositories {
    flatDir(dir: 'path-to-directory', name: 'the-name')
}
```
