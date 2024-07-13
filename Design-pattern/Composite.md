# Composite pattern

## Usage

The composite pattern allows us to compose objects in tree structures then work with these structures as if they were individual objects.

Examples: 

* Components in graphic app can be considered as `Component` . A `Component` can be a specific element like `Dot`, `Line`, `Circle` or can be a `CompositeComponent` that contains other component.

* A delivery service can deliver boxes or products. A box can contain smaller boxes or products. Each smaller boxes can contains smaller box.

## Structure

![](.\images\composite.png)

* Component interface would describe the common operations for both specific component and the container/complex component of the tree

* The Leaf is a specific component that doesn't have sub-components. It would also do the real work.

* The container (AKA composite) is a component that have sub-components. It doesn't know about the concreate class of its children, only work with them via their interface. After receiving a request, a container delegates the work to its children, then sums up the result, does some intermediate work and then returns the final result.
