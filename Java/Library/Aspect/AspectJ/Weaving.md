Weaving is the process of linking aspects with object.

** Note :** To run an AspectJ program, it is required to have `aspectjrt` dependency as a runtime library.

There can be:
## Compile time weaving,
Using plugin `aspectj-maven-plugin`.
```xml
 <plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>aspectj-maven-plugin</artifactId>
    <version>1.11</version>
    <configuration>
        <showWeaveInfo>true</showWeaveInfo>
        
        <!-- Have to specify the java version for this plugin-->
        <complianceLevel>1.8</complianceLevel>
        <source>1.8</source>
        <target>1.8</target>
    </configuration>
    <executions>
        <execution>
            <goals>
                <goal>compile</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```
## Post compile weaving, or binary weaving
This also use `aspectj-maven-plugin` to weave existing class and jar files.  
The jar files must be listed in `<weaveDependencies/>` tag in configuration of the plugin.

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>aspectj-maven-plugin</artifactId>
    <configuration>
        <weaveDependencies>
            <weaveDependency>  
                <groupId>org.group</groupId>
                <artifactId>to-weave</artifactId>
            </weaveDependency>
        </weaveDependencies>
    </configuration>
</plugin>
```
## Loadtime weaving
It is post compile weaving got postponed until the class have been loaded.  
To enable this, `aspectjweaver` must be specified as javaagent.  
It is configured in AOP.xml file.