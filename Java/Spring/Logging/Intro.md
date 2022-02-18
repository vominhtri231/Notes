# Logging

Spring boot has a `LoggingSystem` abstraction that will try to configure logging base on content of the classpath.  
The default logging library would be Logback.  

`Logback` <--- `spring-boot-starter-logging` <--- `spring-boot-starter-web`

## Configuration

You could config logging with some pre-defined properties in application properties.  
Or you could config more precisely by native configuration (such as classpath:logback.xml for Logback).

```properties
# set log level
logging.level.org.springframework.web=DEBUG
logging.level.org.hibernate=ERROR

# set log file
logging.file=/logs/spring.log

# set config file
logging.config=config.xml
```

## Use alternative logging library

To use alternative logging module, you must exclude Logback and include the alternative.

For example: to use log4j

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-logging</artifactId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-log4j2</artifactId>
</dependency>
```
