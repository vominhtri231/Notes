# Multiple project build

Gradle supports multiple project build (equivalent for multi-module build in Maven). Each sub-project is consider as a separate project and can have their own `build.gradle` with a mandatory common root `build.gradle`. To find out about the project structure, use the command `gradle projects`.

## `settings.gradle`

The `settings.gradle` file is where we could config the multiple project build as well as all other project configs of the build. It is on the root level of the project like the `build.gradle`. Unlike the `build.gradle`, Gradle evaluated it in the initialize phase and create a Setting object based on it. [See more](How_to_run_gradle.md)

To add sub-project build, we need to including using the `includes` command. The sub-project can have hierarchies and the levels are described using the colon character `:`.
