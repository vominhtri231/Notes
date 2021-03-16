### Definition
Each generic type will have a raw type, the generic type without any information about the type parameters.  Eg: Raw type of `List<E>` is `List`.

### Remark
- Raw type should be avoided, it is only used for backward compatible with the legacy code. If the type parameter is unknown, use the unbound wildcard. Eg: `List<?>`
- It is only appropriate to use raw type in:
    * Class literal. Eg `List.class`, because it is illegal to have `List<String>.class`.
    * instanceof. Eg: `if(xyz instanceof List){}`, because the type parameter is erased at runtime.
