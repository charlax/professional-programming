# Modern JavaScript/TypeScript

Note: run code quickly with https://codesandbox.io/s/

## Quirks

### Printing and interacting with the console

```javascript
// Do not leave console.log in your code! There are linters such as eslint that will check for their absence
console.log("hello");
```

### Comparing scalar, arrays, and objects

#### Always use triple comparators (`===`) instead of double (`==`)

```javascript
// ???
console.assert('1' == 1)

// Better
console.assert(!('1' === 1))
console.assert('1' !== 1)
```

#### Comparing non-scalar

Applied on arrays and objects, `==` and `===` will check for object identity, which is almost never what you want.

```javascript
console.assert({a: 1} != {a: 1})
console.assert({a: 1} !== {a: 1})

const obj = {a: 1}
const obj2 = obj
console.assert(obj == obj2)
console.assert(obj === obj2)
```

Use a library such as [lodash](https://lodash.com/) to properly compare objects and array

```javascript
import _ from 'lodash'

console.assert(_.isEqual({a: 1}, {a: 1}))
console.assert(_.isEqual([1, 2], [1, 2]))
```

### `Object` methods

#### `Object.assign`, spread operator

`Object.assign` (ES 2015)

### `Array` methods

#### `Array.includes` (ES7)

## Object literals, assignment and destructuring

### Objects

```javascript
const toaster = {size: 2, color: 'red', brand: 'NoName'};

// Get one object key
const {size} = toaster;
console.assert(size === 2)

// Get the rest with ...rest
const {color, brand, ...rest} = toaster;
console.assert(_.isEqual(rest, {size: 2}));

// Set default
const {size2 = 3} = toaster
console.assert(size2 === 3)

// Rename variables
const {size: size3} = toaster
console.assert(size3 === 2)

// Enhances object literals
const name = 'Louis'
const person = {name}
console.assert(_.isEqual(person, {name: 'Louis'}))

// Dynamic properties
const person2 = {['first' + 'Name']: 'Olympe'}
console.assert(_.isEqual(person2, {firstName: 'Olympe'}))
// Btw, you can include quotes although nobody does this
console.assert(_.isEqual(person2, {'firstName': 'Olympe'}))
```

### Array

```javascript
const theArray = [1, 2, 3];
const [first, second] = theArray;
const [first1, second2, ...rest] = theArray;

console.assert(first === 1);
console.assert(second === 2);
console.assert(_.isEqualWith(rest, [3]));
```

## `let` and `const`

```javascript
const constantVar = 'a';

// Raises "constantVar" is read-only
constantVar = 'b';

let mutableVar = 'a';
mutableVar = 'a';

// Note: this will work ok
const constantObject = {a: 1}
constantObject.a = 2
constantObject.b = 3

// Raises: "constantObject" is read-only
constantObject = {a: 1}

// const and let are block scoped. A block is enclosed in {}
{
  const a = 'a';
  console.log({a})
}
// Raises: ReferenceError: a is not defined
console.log({a})
```

Note: try to use `const` as much as you can.

- More constraints = safer code
- Some kind of "immutability" is good (since `const` objects can be modified, it is not true immutability)
- You can't define a `const` without providing its initial value
- Most people do this in modern JS

Never use `var`:

- `var` variables are initialized with `undefined`, while `let` and `const` vars are not initialized and will raise an error if used before definition.
- `var` is globally or function-scoped, depending on whether it is used inside a function.
- `let` and `const` are block-scoped
- `let` and `const` cannot be reused for the same variable name

## Arrow functions

The first advantage of arrow function is that they're shorter to write:

```javascript
// You can define a function this way:
const myFunction = function() {
  console.log("hello world");
}

// With an arrow function, you save a few characters:
const myArrowFunction = () => {
  console.log("hello world");
}

// Some things, like params parentheses, and function code brackets, are optional
const myFunctionToBeShortened = function(a) {
  return a;
}

// Shorter arrow function
const myFunctionToBeShortenedArrowV1 = (a) => {
  return a;
}

// Shortest arrow function
// Remove single param parenthesis, remove function code bracket, remove return
const myFunctionToBeShortenedArrowV2 = a => a
console.assert(myFunctionToBeShortenedArrowV2(1) === 1)
```

### How `this` works in arrow functions

### Best practices

- I usually keep the parameters parenthesis. If you add a parameter, you'll have to add them back.

## Classes

### Prototypal inheritance

## Template literals

### Template tags

## Loops

### `for... of`

Note: prefer using some functional constructs such as `map`, `reduce`, etc.

## Promises

### Creating a promise

### Consuming a promise

### Chaining promises

## Async functions

## Modules

CommonJS syntax:

ES Module syntax:

- default export and imports
- renaming imports

## TypeScript

### Differences between TypeScript and JavaScript

### An introduction to TypeScript's type system

## References

- [ES5 to ESNext — here’s every feature added to JavaScript since 2015](https://www.freecodecamp.org/news/es5-to-esnext-heres-every-feature-added-to-javascript-since-2015-d0c255e13c6e/)
