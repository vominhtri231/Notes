# Object

## Type in JS



There are 6 types in JS: `string`, `number` , `boolean` , `object` , undefined and null.

`string`, `number`, `boolean` are object types that are immutable.
 Plain objects, functions or arrays are also objects. The different is that they are mutable.

## Using object

Objects in JS are collections of property - value mapping. Property's type would be `string` and value's type can be any. If the property is a valid JS name, the quotation can be omitted.

Object declaration in JS does not required a class, we would create them via `object literal`. 

```js
student = {
    'first-name': 'Join'
    last_name: 'Doe'
}
```

To access a property

```js
student['first-name'] // Join
student.last_name // Doe
```

To remove a property

```js
delete student['first-name']
delete student.last_name
```

To add a property

```js
student.grade = 7
student['phone-number'] = 333444555

```

To enumerate object's properties, we can use `for in` syntax. Notice that property can in any order.

```js
for(property in student){
    console.log(property+':'+ student[property])
}
```

## Prototype

Every object is linked to a prototype object that it can inherit property from. All object literals are linked to `Object.prototype`.

To create an object and specify the object should be its prototype, we can use `Object.create`

```js
const person = {
  greet() {
    console.log("hello!");
  },
};

const carl = Object.create(person);
carl.greet();
```

The prototype link only works on retrieval. 

- When we retrieve an property on a object. If the object itself lacks the property, 

JS would retrieve from the prototype object and so on, until the process bottoms out

with `Object.property` => To check if a property is from the actual object, not the prototype , we can use `hasOwnProperty` method

* When we update/delete an property on a object, it would have no affect to the prototype

The prototype relationship is dynamic, meaning if we change a prototype, that change will be visible in all of the objects that based on it.  
