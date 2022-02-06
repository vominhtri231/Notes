# How to run Gradle

```sh
gradle <task> [parameters] [-x <ignore-task>]
```

## Tasks

Task could be written in camel shorten form, as long as they are unique. Eg: yellGradle0 -> yG0

Some help task:

* tasks : show all tasks including their description and group by their group
* properties: show all properties of project

## Parameters

Some useful parameters:

* Logging options:
  -i --info change log level to INFO;
  -s --stacktrace print the stack trace when error;
  -q --quite reduce the log messages
* Others:
  -h -? --help for held menu
  -b --build for choosing different build file
  --offline for build in offline mode ( only check for dependencies in local)

## Running phases

Every gradle command run in 3 phases:

```txt
Initialize phase ----- > Configuration phase -----> Execution phase 
```

In the initialize phase, Gradle will tried to find the settings file in upper level folders. If no settings files are found, the project is considered a single project. You could also set the settings file (using `-c` or `--setting-files`) or tell gradle not to search upward (using `-u` or `--no-search-upward`).
