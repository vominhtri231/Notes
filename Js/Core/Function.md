# Function

Functions in JS are **lexical scoping**, meaning that a inner function can contains reference to the outer function even if the outer function is returned. This is technique is also called **closure**.

When a function is invoked, it will receive 2 hidden parameters: `this` and `arguments`

## Invocation

There are 4 type of invocations:

### Method invocation

If a function is a property of a object, it is called `method`. 
Once it is invoked, the `this` param would be the object that contains it, allow us access object context. Once a method to it, it is called public method. 
`this` param would be resolved that the invocation time, making it highly reusable.

```js
var objectA = {
    value: 0
    increase: function() {
        this.value++;
    }
}
objectA.increase() // value = 1
```

### Function invocation

```js
var sum = add(3,4)
```

The function invocation's `this` param would be the global object. 
This is a mistake of JS. If a inner function is invoke, the `this` param should be `this` of the outer function, then inner function may help outer function to do its job.
To solve the problem, we may create a variable point to the outer function `this` param and access it from the inner function. By convention, it is named `that`.

```js
objectA.double = function() {
    var that = this;
    function helper() {
        that.value = that.value * 2 
        // `that` object is point to `this` object of double method, which point to objectA
    }
    helper();
}
```

### Apply invocation

Since function is also a object, it can have methods, one of them is the `apply` method.
The `apply` method help us to invoke the function, which have 2 parameters. The fist one is `this`, the second one is `parameters`.

```js
function getValue() {
    return this.value;
}
var objectA = {
    value: 1
}
getValue.apply(objectA);
```

### Contructor invocation