# Generator function

## Definition

A generator function is a function that produces a series of values instead of one value. It would return a Generator, which can be iterated.

```js
function* generator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = generator(); // "Generator { }"

console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

## Usages

The generator function can be used to:

- Create infinite data stream
- Better async call
- Implement iterable
