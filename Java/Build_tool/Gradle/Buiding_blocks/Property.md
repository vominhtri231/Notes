# Properties

## Gradle properties

These settings can be use in the gradle script. (Not in the JVM)

They are set via (first one found has higher priority):

- command line `-P` or `--project-prop`
- system property with prefix `org.gradle.project`, eg: `org.gradle.project.foo=bar`
- environment variable with prefix `ORG_GRADLE_PROJECT`, eg: `ORG_GRADLE_PROJECT_foo=bar`
- gradle.properties in project root
- gradle.properties in GRADLE HOME
- gradle.properties in gradle installation directory

They can be use directly: `println abc`

## System properties

These settings can be used in the JVM and are set using:

- command line -D
- gradle file with prefix `systemProp`, eg: `systemProp.foo=bar`

They can be used in the gradle script also: `println System.properties['foo']`
