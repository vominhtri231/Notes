## Introduction
Profiles contain a subset of elements available in the POM, which could be activated/ deactivated  
=> To make build results vary, make it portable.  
Profile could be defined in project level or setting level.
## Activation
1. In command
```sh
    mvn plugin -P profile-1, !profile-2
```
2. Setting default profile
```xml
  <activeProfiles>
    <activeProfile>profile-1</activeProfile>
  </activeProfiles>
```
Set active default for each profile:
```xml
<profiles>
  <profile>
    <id>profile-1</id>
    <activation>
      <activeByDefault>true</activeByDefault>
    </activation>
    ...
  </profile>
</profiles>
```
3. Activation with condition

For property: (can be activate by command like `-Denvironment=test`)
```xml
<property>
    <name>environment</name>
    <value>test</value>
</property>
```
For missing file:
```xml
<file>
    <missing>target/generated-sources/axistools/wsdl2java/org/apache/maven</missing>
</file>
```
For jdk:
```xml
<jdk>[1.3,1.6)</jdk>
```
For OS:
```xml
<os>
    <name>Windows XP</name>
    <family>Windows</family>
    <arch>x86</arch>
    <version>5.1.2600</version>
</os>
```