![](https://logging.apache.org/log4j/2.x/images/Log4jClasses.jpg)

* The application want to use the logger has to request it from the LogManager/LoggerFactory which will select the approriate LoggerContext to obtain the logger.
* The logger will be associate with the LoggerContext with the same name/ package or the root context.
* Each logger context have an active configuration, contains all appenders, context-wide filter, etc.

```properties
#The root logger context, named `stdout`
log4j.rootCategory=INFO, stdout
#Config for stout logger context
log4j.appender.stdout=org.apache.log4j.ConsoleAppender

# the `org.springframework.batch` logger context, named `batchLog`
log4j.logger.org.springframework.batch=INFO, batchLog
#Config for `batchLog` logger context
log4j.appender.batchLog=org.apache.log4j.DailyRollingFileAppender
log4j.appender.batchLog.File=./amazon-s3-upload/log/amazon-s3-upload-info.log
log4j.appender.batchLog.DatePattern='.'yyyyMMdd
log4j.appender.batchLog.Encoding=UTF-8
log4j.appender.batchLog.layout=org.apache.log4j.PatternLayout
log4j.appender.batchLog.layout.conversionPattern=%d{yyyy-MM-dd_HH:mm:ss.SSS} [%p][%c] - <%m>%n
#The filter for the `batchLog` logger context
log4j.appender.batchLog.filter.a=org.apache.log4j.varia.LevelMatchFilter
log4j.appender.batchLog.filter.a.LevelToMatch=INFO
log4j.appender.batchLog.filter.a.AcceptOnMatch=true
log4j.appender.batchLog.filter.b=org.apache.log4j.varia.LevelMatchFilter
log4j.appender.batchLog.filter.b.LevelToMatch=WARN
log4j.appender.batchLog.filter.b.AcceptOnMatch=true
log4j.appender.batchLog.filter.c=org.apache.log4j.varia.DenyAllFilter
...
```