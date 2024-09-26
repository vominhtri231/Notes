# Attribute visible

## Private attribute

In python, there is no `private` keywork, instead of that , we create a attribute in the form `__xyz` or `__xyz_` (2 leading underscore with no 2 trailing underscore).

The language would do `name mangling` to those attribute, by adding a underscore and the class name at the beginning of the variable. For example if the class `Student` has the private attribute `__name`, it will be converted into `_Student__name`. This would ensure that a class's private attribute would not clash with its superclass's private attribute.

**Note**: The converted private attribute is still accessible, so private attribute in python is just a safely mechanism, not a security one.

## Protected attribute

Just like private attribute, there is no real `protected` keywork for protecting a attribute, instead, we would add a leading underscore for a attribute to indicate that it is protected (e.g. `_abc`).

The one leading underscore has no special meaning to the language, it's just a convention that the attribute should not be accessed outside the class.
