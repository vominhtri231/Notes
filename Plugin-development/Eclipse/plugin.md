# Plugin

In eclipse, a plugin will connect with a universe of plugins to form the application. It similars to object in OOP, when a object connects with others to form the system.

## `MANIFEST.MF`

The `MANIFEST.MF` is the bundle manifest of the plugin. It contains importance details of the plugin, such as name, id, version number, dependencies, etc.

## `plugin.xml `

The `plugin.xml` file is the plug-in manifest file of the plugin, can contain information about:

- How to display the plugin including icons, menu items, etc.
- The plugin class (a subclass of org.eclipse.core.runtime.Plugin) and runtime jar.
- [Extensions and extension points](./Extensions-extension_points.md) - how it extends the existing application and how it can be extended.
