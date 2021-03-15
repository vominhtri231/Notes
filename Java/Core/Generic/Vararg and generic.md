#### Introduction
``` java
	Arrays.asList(T...list);
```
When invoke a varagr method, an array is created to hold the variables. Since array not work well with generic, we have the same problem with vararg. The problem is when it is illegal to create an array of non-reified, it is legal to vararg. If this happen:
 - A warning `HEAP POLLUTION` is emit in the delair side
 - A warning `UNCHECKED` is emit on every call sides  

=> Writer of this class could use `SuppressWarning('safeVarargs')` to prevent compiler from emit these warnings but you have to make sure that the method is actually safe by:
1. Not save anything to the vararg array
``` java
	void dangerous(List<String>... stringLists) {
        Object[] objects = stringLists;
        objects[0] = Lists.of(42);
        String s = stringLists[0].get(0); // throw ClassCastException
    }
```
2. Not export the vararg parameter array
``` java
    // Dangerous!
	<T> T[] toArray(T... args) {
        return args;
    }

    <T> T[] toArray2Parameters(T a, T b) {
        return toArray(a, b);
    }

	String[] a = toArray("a","b") // ok
    String[] b = toArray2Parameters("a", "b"); // throw ClassCastException
	// In case b, an error is throw because #toArray2Parameters has to
	// allocate an Object[] array to pass parameters to #toArray
	// (the type of parameters is unkown - this is to gurantee the type)
	// While in case a, the type is know, compiler would allocate a String[] array
```






   
    