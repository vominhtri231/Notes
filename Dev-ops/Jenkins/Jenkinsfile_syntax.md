# Jenkins file syntax

Jenkins support 2 types of syntaxes:

## Scripted

Write the whole pipeline using plain groovy script, allow high flexibility but difficult

```groovy
node { 
    stage ('prepare') {
        // M3 maven tool must be configured in the global configuration
        mvnHome = tool 'M3'
    }

    stage ('build') {
        // the work for the stage
        sh 'echo $JAVA_HOME'
    }
}
```

## Declarative

Write the pipeline with pre-defined structure, easier but not as powerful

```groovy
pipeline {
    // the node that execute the pipeline - relevant for cluster setup
    agent any

    // setup tools for running the pipeline
    tools {
        // M3 maven tool must be configured in the global configuration
        maven 'M3'
    }

    // where the work happens
    stages {  
        stage ('build') {
            // the condition for running the stage
            when {
                expression {
                    env.BRANCH_NAME == 'dev'
                }
            }

            // the work for the stage
            steps {
                sh 'echo $JAVA_HOME'
            }
        }
    }

    // run after the pipeline is done
    post {
        always { ... }
        success { ... }
    }
}
```
