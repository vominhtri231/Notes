## Intro
* Maven is a plugin execution framework, every action in Maven is done by plugins.
* There are 2 kinds of plugin in Maven:
    1. Build: is declared inside `<build/>` block
    2. Report: is declared inside `<reporting/>` block
* You can use plugins that is supported by the maven project, 3rd-party plugins (at MojoHaus or any other sources) or write one.

## Write plugin
The customized plugin should be named `<yourplugin>-maven-plugin`.  
The Mojo (Maven-old-java-object) is the goal of the plugin.

```java
package sample.plugin;
...

@Mojo( name = "sayhi")
public class GreetingMojo extends AbstractMojo
{
    public void execute() throws MojoExecutionException
    {
        getLog().info( "Hello world." );
    }
}
```

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
 
  <groupId>sample.plugin</groupId>
  <artifactId>hello-maven-plugin</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>maven-plugin</packaging>
 
  <name>Sample Parameter-less Maven Plugin</name>
  ...
</project>
```

## Execute the plugins
* Directly
```sh
mvn plugin-name
```
* Attach to build lifecycle by `executions` tag
```xml
<plugin>
    ...
    <executions>
      <execution>
        <phase>compile</phase>
        <goals>
          <goal>sayhi</goal>
        </goals>
      </execution>
    </executions>
</plugin>
```
**Note:** If the goal don't have the default phase, and the phase is not specified, it will not get executed at all.
## Some common plugins
* exec: To execute a project (execute only)   
  Eg: `mvn exec:java  -Dexec.mainClass=test.Main`