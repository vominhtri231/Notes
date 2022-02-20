# Environment variable

Jenkins environment variable is a global variable than can be accessed via `env` anywhere in the Jenkins file.  

The `env` variable save data as key-value form, as value is String.

## List all environment variables

1. File `${YOUR_JENKINS_HOST}/env-vars.html` contains all predefined environment variables
2. Via `printenv` shell command

``` groovy
sh 'printenv'
```

## Read environment variables

Environment variable can be accessed via `env`, eg: `env.VARIABLE_NAME`.
Or you could access `VARIABLE_NAME` directly.

## Set environment variables

You could set environment via `environment` block, `env.VARIABLE_NAME` or using `withEnv(["VARIABLE_NAME=value"]) {}`.

The override order is `withEnv`, `environment`, `env`.  
Eg: `withEnv` could override every environment variable, `env.VARIABLE_NAME=...` could only override environment set by another `env.VARIABLE_NAME=...`.

``` groovy
environment {
  TEST_VARIABLE = "Alan"
}
// TEST_VARIABLE changed from here
steps {
  script {
    env.TEST_VARIABLE = "Bob"
  }
  // TEST_VARIABLE changed from here

  withEnv(["A_ENV_VAR=123","ANOTHER_ENV_VAR=abc"]) {
    // ANOTHER_ENV_VAR changed in here only
  }
}
```
