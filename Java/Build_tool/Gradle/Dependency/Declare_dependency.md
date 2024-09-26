# Declare dependency

## External dependency

```groovy
dependencies {
    configurationName name: 'name', group: 'group', version: 'version'
    configurationName 'group:name:version'

    // exclude specific transitive dependency
    configurationName 'group:name:version' {
        exclude group: 'group', module: 'name' 
    }

    // force version for the specific dependency
     configurationName 'group:name:version' {
        force 'group:name:version' 
    }

    // exclude all transitive dependency
    configurationName 'abc' {
        transitive = false 
    }
    
    // specical version select
    // select the latest version
    configuration name: 'name', group: 'group', version: 'latest-integration'
    // select version greater than 1.0
    configuration name: 'name', group: 'group', version: '1.+' 
    // select version greater than 1.0 than less than 1.3
    configuration name: 'name', group: 'group', version: '1.+ -> 1.3' 
}
```

## File dependency

```groovy
dependencies {
    configurationName fileTree(dir: 'the-directory', include: '*.jar')
}
```
