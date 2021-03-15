Repository is the place to store the build artifacts and cache dependancies.  
There are 2 types of repositories:
1. Local
2. Remote:   
   By default maven will use the [central](https://repo.maven.apache.org/maven2/) repository, which is defined in [Super POM](https://maven.apache.org/ref/3.6.3/maven-model-builder/super-pom.html). You could specify `mirror` or other repository to override this behavior. To build maven offline: `mvn -o package`.