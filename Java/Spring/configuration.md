# Configuration

## Parse configuraion as object

Configurations can be parsed as object via annotation `@ConfigurationProperties`. The object will scan for all properties with the same prefix. From spring 2.2, configuration properties is considered as component.

```java
@ConfigurationProperties(prefix = "mail")
public class ConfigProperties {
    
    private String hostName;
    private int port;
    private String from;
}
```
