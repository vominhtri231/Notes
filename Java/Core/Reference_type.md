# Reference types

## Strong reference

The most common type reference that we usually use. Any object which as a strong reference pointing to it is not eligible for GC.

```java
Object obj = new Object();
```

## Soft reference

An object has a soft reference pointing to it will not be garbage collected until the JVM absolutely needs memory.

```java
Object obj = new Object();  
SoftReference<Object> soft = new SoftReference<Object>(obj); 
obj = null; 
// even when obj is null now, its memory won't be collected
// until JVM needs memory 
```

## Weak reference

An object only has week reference will be garbage collected eagerly in the next GC cycle.

```java
Object obj = new Object();  
WeakReference<Object> soft = new WeakReference<Object>(obj); 
obj = null;
```

The week reference are used as key in `WeakHashMap` , make it an efficient memory cache.
