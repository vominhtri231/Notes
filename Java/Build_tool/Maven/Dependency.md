# Dependency

## Dependency mediation

If there are multiple versions of the same artifact, maven would pick the **nearest dependency** (dependency with the lower depth). If there are multiple versions with the same depth, then the first one to be declared would be used.

Eg: In this case artifact D with version 1.0 will be used.

```txt
  A
  |-- B
  |   |-- C
  |       |-- D 2.0
  |-- E
      |-- D 1.0
```

## Dependency scopes

Scopes used to determine when a dependency is included. There are 6 scopes:

1. Compile (default)
2. Provided - Indicate that the JDK or container will provide the dependency
3. Runtime
4. Test
5. System - Indicate that you will provide the JAR explicitly
6. Import - Only supported of type `<pom>` in the `<dependencyManagement>` and will be replaced by the effective one

## Dependency management

It a mechanism for centralizing dependency information. 
When you have a set of projects inherit from a common project,
you could put all information about the dependencies in the parent pom and have simple reference to the dependencies in the child pom.

Eg:
In parent pom:

```xml
<dependencyManagement>
    <dependencies>
        <dependency> 
            <groupId>group-a</groupId>
            <artifactId>artifact-a</artifactId>
            <version>1.0</version>
 
            <exclusions>
              <exclusion>
                <groupId>group-c</groupId>
                <artifactId>excluded-artifact</artifactId>
              </exclusion>
            </exclusions>
        </dependency>
        ...
    </dependencies>
</dependencyManagement>
```

In child pom:

```xml
<dependencies>
    <dependency>
      <groupId>group-a</groupId>
      <artifactId>artifact-a</artifactId>
    </dependency>
    ...
</dependencies>
```
