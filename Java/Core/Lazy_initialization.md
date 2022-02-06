# Lazy initialization

## Usage

Lazy initialization is used to:

1. Break circular initialization
2. Improve performance  

For performance reason, you should consider the cost of initializing, the cost of access the field, how many time access the field

## Idioms

### Synchronized accessor

Should be used to break circular initialization

```java
private FieldType field;

synchronized FieldType getField() {
    if(field == null){
        field = computeField();
    }
    return field;
}
```

### Holder class

Can only be used for static fields. This base on the guarantee that a class will not be initialized until it is used.  
The beauty of this approach is that getField() method is not synchronized. Once the class is initialized, the VM patches the code so that subsequent access to the field does not involve any testing or synchronization.

```java
private static class FieldHolder {
    static final FieldType field = computeField();
}

static FieldType getField() {
    return FieldHolder.field;
}
```

### Double-check

Can be used for instance fields.

```java
private volatile FieldType field;

FieldType getField() {
    if (field == null) {
        synchronized(this) {
            if ( field == null ) {
                field = computeField():
            }
        }
    }
    return field;
}
```
