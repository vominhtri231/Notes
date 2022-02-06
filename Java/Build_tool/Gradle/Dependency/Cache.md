# Cache

## Where

The caches are saved under `<USER-HOME>/.gradle/caches`.

Structure of caches is changed on each version. On version 6+, artifacts are saved under `module-2/files-<>/`, metadata are saved under `module-2/metadata-<>` and resources are saved under `module-2/resource-<>`.

## How

Each item is saved under a directory which name is the SHA of the item. This allow gradle to detect changes of the same version.

Each version would have a cache time, after it is expired, Gradle will check again for any changes. You could force Gradle to check by flag `--refresh-dependencies` and force it not to by `--offline`.
You could also configure the cache time.

```groovy
configurations.implementation.resolutionStrategy {
    cacheDynamicVersionFor 10, 'seconds' // set cache time for dynamic version dependencies
    cacheChangingModulesFor 10, 'seconds' // set cache time for snapshot version dependencies
}
```
