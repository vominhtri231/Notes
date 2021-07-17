# How to run Gradle

```shell
gradle <task> [parameters] [-x <ignore-task>]
```

## Tasks

Task could be written in camel shorten form, as long as they are unique. Eg: yellGradle0 -> yG0

Some help task:

* tasks : show all tasks including their description
* properties: show all properties of project

## Parameters

Some useful parameters:

* Properties options:
  -D system property;
  -P project property, available in the build script
* Logging options:
  -i --info change log level to INFO;
  -s --stacktrace print the stack trace when error;
  -q --quite reduce the log messages
* Others:
  -h -? --help for held menu
  -b --build for choosing different build file
  --offline for build in offline mode ( only check for dependencies in local)
