## Day 14

I learned more about Generators.

They are special functions that can pause their execution and resume later, producing multiple values on demand.

They are defined using the `function*` syntax.

An iterator that has a `next()` method for consuming the yielded values. It also conforms to the iterable protocol.

There's also `yield` keyword which pauses the generator function's execution and returns a value to the caller. When
`next()` is called again, execution resumes from the point of the last yield.

Example:

```
function* simpleGenerator() {
  yield 1;
  yield 2;
  yield 3;
}

const generator = simpleGenerator();

console.log(generator.next()); // Output: { value: 1, done: false }
console.log(generator.next()); // Output: { value: 2, done: false }
console.log(generator.next()); // Output: { value: 3, done: false }
console.log(generator.next()); // Output: { value: undefined, done: true }
```
