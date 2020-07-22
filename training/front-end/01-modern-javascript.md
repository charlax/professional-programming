<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of Contents

- [Modern JavaScript](#modern-javascript)
  - [Quirks](#quirks)
    - [Undefined everywhere!](#undefined-everywhere)
    - [Printing and interacting with the console](#printing-and-interacting-with-the-console)
    - [Comparing scalar, arrays, and objects](#comparing-scalar-arrays-and-objects)
      - [Always use triple comparators (`===`) instead of double (`==`)](#always-use-triple-comparators--instead-of-double-)
      - [Comparing non-scalar](#comparing-non-scalar)
    - [`Object` methods](#object-methods)
      - [`Object.assign`, spread operator](#objectassign-spread-operator)
    - [`Array` methods](#array-methods)
      - [`Array.includes` (ES7)](#arrayincludes-es7)
  - [Object literals, assignment and destructuring](#object-literals-assignment-and-destructuring)
    - [Objects](#objects)
    - [Array](#array)
  - [`let` and `const`](#let-and-const)
    - [Hoisting](#hoisting)
  - [Arrow functions](#arrow-functions)
    - [How `this` works in arrow functions](#how-this-works-in-arrow-functions)
    - [Best practices](#best-practices)
  - [Classes](#classes)
    - [Prototypal inheritance](#prototypal-inheritance)
  - [Template literals](#template-literals)
    - [Template tags](#template-tags)
  - [Loops](#loops)
    - [`for... of`](#for-of)
  - [Promises](#promises)
    - [Creating a promise](#creating-a-promise)
    - [Consuming a promise](#consuming-a-promise)
    - [Chaining promises](#chaining-promises)
  - [Async functions](#async-functions)
  - [Modules](#modules)
  - [Other features](#other-features)
    - [Optional chaining](#optional-chaining)
  - [References](#references)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Modern JavaScript

Note: run code quickly with https://codesandbox.io/s/

## Quirks

### Undefined everywhere!

There are no required arguments in JavaScript:

```javascript
function hello(name) {
  return name;
}

// No raise, will log "undefined"
console.log(hello());

// Here's how to compare to undefined
console.assert(typeof undefined === "undefined");
```

### Printing and interacting with the console

```javascript
// Do not leave console.log in your code! There are linters such as eslint that will check for their absence
console.log("hello");
```

### Comparing scalar, arrays, and objects

#### Always use triple comparators (`===`) instead of double (`==`)

```javascript
// ???
console.assert("1" == 1);

// Better
console.assert(!("1" === 1));
console.assert("1" !== 1);
```

#### Comparing non-scalar

Applied on arrays and objects, `==` and `===` will check for object identity, which is almost never what you want.

```javascript
console.assert({ a: 1 } != { a: 1 });
console.assert({ a: 1 } !== { a: 1 });

const obj = { a: 1 };
const obj2 = obj;
console.assert(obj == obj2);
console.assert(obj === obj2);
```

Use a library such as [lodash](https://lodash.com/) to properly compare objects and array

```javascript
import _ from "lodash";

console.assert(_.isEqual({ a: 1 }, { a: 1 }));
console.assert(_.isEqual([1, 2], [1, 2]));
```

### `Object` methods

#### `Object.assign`, spread operator

`Object.assign` (ES 2015)

### `Array` methods

#### `Array.includes` (ES7)

## Object literals, assignment and destructuring

### Objects

```javascript
const toaster = { size: 2, color: "red", brand: "NoName" };

// Get ("destructure") one object key
const { size } = toaster;
console.assert(size === 2);

// Note: this also works with functions
function destructuredFunction({ color }) {
  return color;
}

console.assert(destructuredFunction({ color: "red" }) === "red");

// Get the rest with ...rest
const { color, brand, ...rest } = toaster;
console.assert(_.isEqual(rest, { size: 2 }));

// Set default
const { size2 = 3 } = toaster;
console.assert(size2 === 3);

// Rename variables
const { size: size3 } = toaster;
console.assert(size3 === 2);
```

Enhanced object literals:

```javascript
const name = "Louis";
const person = { name };
console.assert(_.isEqual(person, { name: "Louis" }));

// Dynamic properties
const person2 = { ["first" + "Name"]: "Olympe" };
console.assert(_.isEqual(person2, { firstName: "Olympe" }));
// Btw, you can include quotes although nobody does this
console.assert(_.isEqual(person2, { firstName: "Olympe" }));

// Short form function
const es5Object = {
  say: function () {
    console.log("hello");
  },
};
es5Object.say();

const es6Object = {
  say() {
    console.log("hello");
  },
};
es6Object.say();

// Prototype and super()
const firstObject = {
  a: "a",
  hello() {
    return "hello";
  },
};

const secondObject = {
  __proto__: firstObject,
  hello() {
    return super.hello() + " from second object";
  },
};

console.assert(secondObject.hello() === "hello from second object");
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
const constantVar = "a";

// Raises "constantVar" is read-only
constantVar = "b";

let theVar = "a";
theVar = "a";

// Note: this will work ok
const constantObject = { a: 1 };
constantObject.a = 2;
constantObject.b = 3;

// Raises: "constantObject" is read-only
constantObject = { a: 1 };

// const and let are block scoped. A block is enclosed in {}
{
  const a = "a";
  console.log({ a });
}
// Raises: ReferenceError: a is not defined
console.log({ a });
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

### Hoisting

See [Hoisting on MDN](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)

## Arrow functions

The first advantage of arrow function is that they're shorter to write:

```javascript
// You can define a function this way:
const myFunction = function () {
  console.log("hello world");
};

// With an arrow function, you save a few characters:
const myArrowFunction = () => {
  console.log("hello world");
};

// Some things, like params parentheses, and function code brackets, are optional
const myFunctionToBeShortened = function (a) {
  return a;
};

// Shorter arrow function
const myFunctionToBeShortenedArrowV1 = (a) => {
  return a;
};

// Shortest arrow function
// Remove single param parenthesis, remove function code bracket, remove return
const myFunctionToBeShortenedArrowV2 = (a) => a;
console.assert(myFunctionToBeShortenedArrowV2(1) === 1);
```

### How `this` works in arrow functions

### Best practices

- I usually keep the parameters parenthesis. If you add a parameter, you'll have to add them back.

## Classes

```javascript
class Toaster {
  constructor(color) {
    this.color = color;
  }

  dring() {
    return "dring";
  }
}

// Don't forget new!
// Raises: TypeError: Cannot call a class as a function
// const toaster = Toaster('red');

const toaster = new Toaster("red");
console.log(toaster.dring());

// Inheritance

class BunToaster extends Toaster {
  dring() {
    return super.dring() + " dring";
  }
}

const bunToaster = new BunToaster("red");
console.assert(bunToaster.dring() === "dring dring");
```

Those are my opinions about other class features:

- Avoid using `static` methods, use plain functions instead.
- Avoid using more than one level of inheritance.
- Avoid using getter and setters (`get` and `set`).
- Avoid using classes altogether.

### Prototypal inheritance

## Template literals

```javascript
const longString = `multi
line
string`;

const name = "Louis";
// Template interpolation
const hello = `Hello ${name}`;

// You can have expressions
const hello1 = `Hello ${name + "!"}`;
const hello2 = `Hello ${name === "Louis" ? name : "Noname"}`;
```

### Template tags

They are used in some libraries, like Apollo and Styled Components.

```javascript
function templateTag(literals, ...expressions) {
  console.assert(_.isEqual(literals, ["hello ", ""]));
  console.assert(_.isEqual(expressions, [3]));
  return _.join(_.flatten(_.zip(literals, expressions)), "");
}

const result = templateTag`hello ${1 + 2}`;
console.assert(result === "hello 3");
```

## Loops

### `for... of`

Note: prefer using some functional constructs such as `map`, `reduce`, etc.

```javascript
for (const i of [1, 2, 3]) {
  console.log({ i });
}
// 1, 2, 3

for (const key in { a: "aaa", b: "bbb" }) {
  console.log({ key });
}
// 'a', 'b'
```

## Promises

This is only going to be an introduction to the magnificent world of promise.

- Async functions (seen later) use promises as a building block.
- Promise are indeed async in nature: the calling code continues executing the promise does its thing.
- Some Web API return promises, including `Fetch`

### Creating a promise

Note: we use TypeScript in this example, to clarify what's return. You can ignore the type annotations for now.

```typescript
let isDone: boolean = true

const thePromise = new Promise((resolve, reject) => {
  if (isDone) {
    resolve("the work is done");
  } else {
    reject("this is still pending");
    }
    }

console.assert(thePromise === 'the work is done')
```

TODO

### Consuming a promise

### Chaining promises

## Async functions

## Modules

CommonJS syntax:

ES Module syntax:

- default export and imports
- renaming imports

## Other features

### Optional chaining

## References

- [ES5 to ESNext — here’s every feature added to JavaScript since 2015](https://www.freecodecamp.org/news/es5-to-esnext-heres-every-feature-added-to-javascript-since-2015-d0c255e13c6e/)
- [ES2015 / ES6: Basics of modern Javascript](https://www.slideshare.net/WojciechDzikowski/es2015-es6-basics-of-modern-javascript)
