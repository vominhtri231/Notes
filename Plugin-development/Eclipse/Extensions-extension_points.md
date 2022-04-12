# Extension and extension points

In Eclipse, this is the machanism for loose coupling. This allows other plugins to extend or customize the functionality.

An extension point and an extension similar to socket and light bulb. There are variaty of extension points and only extensions designed for that will fit. The extension point will have a contract that the extension have to comform to.

## How to declair extension point

The extension point is decribed via a XML schema file, then linked into the `plugin.xml` file.

```xml
<?xml version="1.0" encoding="utf-8"?>
<?eclipse version="3.2"?>
<plugin>
    <extension-point 
        id="abc.com"
        name="Abc"
        schema="schema/abc.exsd" />
</plugin>
```

## Access extension

The registried extension can be accessed via `IExtensionRegistry` or `Platform.getExtensionRegistry()` (in eclipse 3.X +) of the eclipse runtime.

```java
Platform.getExtensionRegistry().
    getConfigurationElementsFor("extension-id");
```


