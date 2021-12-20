# Declare dependency

## External dependency

```groovy
dependencies {
    configurationName name: 'name', group: 'group', version: 'version'
    configurationName 'group:name:version'

    configurationName 'group:name:version' {
        exclude group: 'group', module: 'name' // exclude specific transitive dependency
    }

     configurationName 'group:name:version' {
        force 'group:name:version' // force version for the specific dependency
        force 'group:name:version' // force version for the specific dependency
    }

    configurationName 'abc' {
        transitive = false // exclude all transitive dependency
    }

    configuration name: 'name', group: 'group', version: 'latest-integration' // will selected the latest version

    configuration name: 'name', group: 'group', version: '1.+' // will selected version greater than 1.0

    configuration name: 'name', group: 'group', version: '1.+ -> 1.3' // will selected version greater than 1.0 than less than 1.3
}
```

## File dependency

```groovy
dependencies {
    configurationName fileTree(dir: 'the-directory', include: '*.jar')
}
```
