## Intro
The techniche that allow injection in only some fields but not all.

## How to
Use `@Assisted` to indicate field's value come from an argument, not injected. The value is later passed to by a Factory.
```java
class Car {
    @Inject
    public Car(final Engine engine, @Assisted final int sits){
        // initialize a car
    }
}

interface CarFactory {
    Car createCar(int sits);
}

// in binding module
install(new FactoryModuleBuilder()
        // if there are multiple implementations of Engine
        .implement(Engine.class, UltraEngine.class)
        .build(CarFactory.class));
```

In call side:
```java
@Inject
CarFactory carFactory;
carfactory.createCar(6);
```

## Remarks
* If the assisted fields have the same type, you could specify the name. Eg:
```java
    @Inject
    public Car(final Engine engine, @Assisted("sits") final int sits,
              @Assisted("windows") final int windows){
        // initialize a car
    }
```