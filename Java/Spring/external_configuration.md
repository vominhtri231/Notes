# External configuration

External configuration is used to work with the same application code in different environments.

## Load order

The properties are considered in the order:

- Command line argument - E.g: `--server.port=9000` 
- JAVA system properties - E.g: `-Dserver.port=9000`
- OS properties - E.g: `set SERVER_PORT=9090`
- `@PropertySource` annotations (yaml not supported yet)
- Application properties outside of jar (including yaml file) 

  By default they are loaded from:
  - From `/config` dir of current directory
  - From the current directory

- Application properties inside of jar (including yml file)

  By default they are loaded from (You could also set the location via config `spring.config.location`):
  - Classpath `/config` dir
  - Classpath root

- Default properties


## Usage

Configurations can be accessed via `@Value`, `Environment` abstraction or bound to structure object via `@ConfigurationProperties`, etc.

### `@ConfigurationProperties`

Configurations can be parsed as object via annotation `@ConfigurationProperties`. The object will scan for all properties with the same prefix. From spring 2.2, configuration properties is considered as component.

```java
@ConfigurationProperties(prefix = "mail")
public class ConfigProperties {
    
    private String hostName;
    private int port;
    private String from;
}
```
