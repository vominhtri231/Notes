### Differences
| Array | Generic |
| :---  | :--- |
| Covarian:  `Sup[]` is a suptype of `Super[]`| Invarian: `List<Sup>` is not a subtype of `List<Super>`|
| Reified: Enforce type at runtime | Erasure: Enforce type at complile time then earse it

=> It is illegal to create array of generic type of type parameter, except for unboned wildcard types.  
Eg: `new List<String>[]`, `new List<E>[]` or `new E[]` are illegal, when `List<?>` is. Because `List<?>` contain the same information as complile time in runtime.

### Why it is illegal to create non-reified array
```java
List<String>[] stringLists = new List<String>[1]; // 1
List<Integer> intList = List.of(42);
Object[] objects = stringLists;
objects[0] = intList;
String s = stringLists[0].get(0); // 2
```
If 1 could compile successfully, 2 would throw `ClassCastException`.

=> Prefer generic to array