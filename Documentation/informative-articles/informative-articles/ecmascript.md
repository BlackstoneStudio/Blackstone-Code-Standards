# ECMAScript

Most important and most used features of each ECMAScript version:


### ECMAScript 2015 (ES6):

#### Arrow functions

Allows you to write functions in a more concise and readable way. For example:

```javascript 
// before ES6
var sum = function(a, b) {
  return a + b;
};

// after ES6
var sum = (a, b) => a + b;
```

#### Template literals

Allows you to insert variable values into a string in a simpler and more readable way. For example:

```javascript 
// before ES6
console.log("My name is " + firstName + " " + lastName);

// after ES6
console.log(`My name is ${firstName} ${lastName}`);

```

#### Destructuring

Allows you to extract values from objects and arrays in a more concise way. For example:

``` 
// before ES6
var person = {firstName: "John", lastName: "Doe"};
var firstName = person.firstName;
var lastName = person.lastName;

// after ES6
var {firstName, lastName} = person;
```

#### Rest/spread properties

The rest and spread properties provide a way to merge or split objects. The spread operator can be used to spread an object's properties into another object, while the rest operator can be used to gather properties into an object.

```javascript 
const object1 = { a: 1, b: 2 };
const object2 = { c: 3, ...object1 };
console.log(object2); // { a: 1, b: 2, c: 3 }

const { a, ...rest } = object2;
console.log(rest); // { b: 2, c: 3 }
```

#### Ternary Operator

The ternary operator is a simplified conditional operator like `if` / `else`.

``` 
// Before
if (authenticated) {
  renderApp();
} else {
  renderLogin();
}

//After
authenticated ? renderApp() : renderLogin();
```

#### Modules

This allows you to divide your code into separate modules and use them in an application. For example:

```javascript 
// in a file named "math.js"
export function sum(a, b) {
  return a + b;
}

export function multiply(a, b) {
  return a * b;
}

// in another file
import { sum, multiply } from "./math";
console.log(sum(1, 2)); // 3
console.log(multiply(1, 2)); // 2
```

#### Classes

Allows you to use a syntax closer to object-oriented languages to define classes. For example:

```javascript 
// before ES6
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}
Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.firstName} ${this.lastName}`);
};

// after ES6
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  sayHello() {
    console.log(`Hello, my name is ${this.firstName} ${this.lastName}`);
  }
}
```

#### Generators

A new type of function that allows you to pause and resume execution, and produce values one at a time. For example:

```javascript 
function* countdown(n) {
  while (n > 0) {
    yield n;
    n--;
  }
}

var counter = countdown(5);
console.log(counter.next().value); // 5
console.log(counter.next().value); // 4
```

#### Promise

An object that represents the eventual completion or failure of an asynchronous operation. It allows you to handle asynchronous operations in a more concise and readable way.

Here is an example of using a Promise to retrieve data from an API:

```javascript 
function getData(url) {
  return new Promise(function(resolve, reject) {
    var xhr = new XMLHttpRequest();
    xhr.open("GET", url, true);
    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4) {
        if (xhr.status === 200) {
          resolve(JSON.parse(xhr.responseText));
        } else {
          reject(xhr.statusText);
        }
      }
    };
    xhr.send();
  });
}

getData("https://api.example.com/data")
  .then(function(data) {
    console.log("Data retrieved:", data);
  })
  .catch(function(error) {
    console.error("Error:", error);
  });
```

In this example, `getData` is a function that returns a Promise that retrieves data from a given URL using an XHR request. The Promise has two callbacks: `resolve` and `reject`. If the XHR request succeeds and the status code is 200, the Promise is resolved with the response text parsed as JSON. If the XHR request fails, the Promise is rejected with the status text.

You can use the `.then` method to register a callback that is executed when the Promise is resolved, and the `.catch` method to register a callback that is executed when the Promise is rejected. In this example, the `.then` callback logs the data, and the `.catch` callback logs the error.

#### Set

Is a data structure that allows you to store unique values. Sets do not allow duplicate elements and provide an easy way to check if an element exists or not.

```javascript 
const set = new Set();
set.add(1);
set.add(2);
set.add(3);

console.log(set.has(1)); // true
console.log(set.size); // 3
```

#### Map

Is a data structure that allows you to store key-value pairs. Keys can be any value (object, number, string, etc.), while values can be anything. Additionally, Maps allow you to access, add, and remove items efficiently.

```javascript 
const map = new Map();
map.set("key1", "value1");
map.set("key2", "value2");

console.log(map.get("key1")); // "value1"
console.log(map.size); // 2
```

#### WeakMap

Is similar to Map, but with some important differences. Key values in a WeakMap can only be objects, and unlike Map, objects used as keys in a WeakMap are not held in memory. This means that if an object used as a key has no active references, it will be automatically disposed of by the JavaScript garbage collector.

```javascript 
const weakMap = new WeakMap();
const obj = {};
weakMap.set(obj, "value");

console.log(weakMap.get(obj)); // "value"
```

### ECMAScript 2016 (ES7):

#### Array.includes

This method returns a boolean indicating whether an array includes a certain element.

```javascript 
const array = [1, 2, 3];
console.log(array.includes(2)); // true
console.log(array.includes(4)); // false
```

#### Exponentiation operator

This operator allows you to perform exponential calculations more easily.

```javascript 
console.log(2 ** 3); // 8
console.log(4 ** 0.5); // 2
```

#### Async/await

This syntax allows you to write asynchronous code that looks and behaves like synchronous code.

```javascript 
async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

fetchData();
```

In this example, `fetchData` is an asynchronous function that fetches data from an API using the `fetch` method. The `await` keyword is used to wait for the results of each asynchronous operation before proceeding to the next. The `try`...`catch` syntax is used to handle errors. The overall effect is that the code looks and behaves like synchronous code, but it is actually asynchronous and does not block the main thread.

### ECMAScript 2017 (ES2017):

#### Object.values/Object.entries

These methods return arrays of an object's values or key-value pairs, respectively.

```javascript 
const object = { a: 1, b: 2, c: 3 };
console.log(Object.values(object)); // [1, 2, 3]
console.log(Object.entries(object)); // [['a', 1], ['b', 2], ['c', 3]]
```

#### String padding

These methods add padding to the beginning or end of a string.

```javascript 
console.log('x'.padStart(5, '-')); // ---x
console.log('x'.padEnd(5, '-')); // x---
```

#### Async functions:

These are complete feature that includes `async/await` syntax, as well as a way to create, return, and consume promises in JavaScript. They provide a way to write asynchronous code that looks and behaves like synchronous code but does not block the main thread.

### ECMAScript 2018 (ES2018):

#### Async iteration

This feature allows for asynchronous iteration over data, such as arrays and maps.

```javascript 
const data = [1, 2, 3, 4, 5];

async function *asyncData() {
  for (const item of data) {
    await new Promise(resolve => setTimeout(resolve, 100));
    yield item;
  }
}

(async () => {
  for await (const item of asyncData()) {
    console.log(item);
  }
})();
```

In this example, `asyncData` is a generator function that yields each item of the `data` array after a 100-millisecond delay. The `for await` loop is used to iterate over the items as they are produced by the generator. The overall effect is that the loop iterates asynchronously over the `data` array.

#### RegExp changes

ES2018 introduced several improvements to regular expressions, including the `s` (dotAll) flag, which allows the dot metacharacter to match newlines, and the `unicode` flag, which enables Unicode mode in regular expressions.

```javascript 
const regex = /.*/s;
console.log(regex.test('foo\nbar')); // true

const regex2 = /\w+/u;
console.log(regex2.test('text')); // true
```

### ECMAScript 2019 (ES2019):

#### Object.fromEntries

This method allows for the creation of an object from a list of key-value pairs

```javascript 
const entries = [['a', 1], ['b', 2]];
const object = Object.fromEntries(entries);
console.log(object); // { a: 1, b: 2 }
```

#### String trimming

ES2019 introduced two new string trimming methods, `String.prototype.trimStart` and `String.prototype.trimEnd`, which allow for the trimming of whitespace characters from the beginning and end of strings, respectively.

```javascript 
const string = '  foo  ';
console.log(string.trimStart()); // 'foo  '
console.log(string.trimEnd()); // '  foo''
```

#### Array.flat/Array.flatMap

These methods allow for flattening arrays to a specified depth.

```javascript 
const array = [1, [2, [3, 4], 5]];
console.log(array.flat()); // [1, 2, [3, 4], 5]
console.log(array.flat(2)); // [1, 2, 3, 4, 5]

const array2 = [1, 2, 3, 4, 5];
console.log(array2.flatMap(x => [x, x * 2])); // [1, 2, 2, 4, 3, 6, 4, 8, 5, 10]
```

### ECMAScript 2020 (ES2020):

#### Optional Chaining

This feature allows for checking for the existence of an object property or method before trying to access it, avoiding errors due to undefined values:

```javascript 
const user = {
  name: 'John',
  address: {
    city: 'New York'
  }
};

console.log(user?.address?.city); // "New York"
console.log(user?.name?.last); // undefined
```

#### Nullish Coalescing

This operator allows for providing a default value when a value is either `null` or 
`undefined`.

```javascript 
const x = null;
const y = undefined;
const z = 0;

console.log(x ?? 42); // 42
console.log(y ?? 42); // 42
console.log(z ?? 42); // 0
```

#### Global this

This feature allows for a value for `this` to be provided in a global context, rather than being undefined. 
The value of `this` is determined by how a function is called. In the global scope, the value of `this` is typically `undefined` in strict mode, and the global object (`window` in web browsers, or `global` in Node.js) in non-strict mode.

```javascript 
console.log(globalThis); // logs the global object (e.g. window or global)
```

#### BigInt

Is a new data type that allows you to represent arbitrarily large numbers. This allows to overcome the limits of representation of numbers in JavaScript

```javascript 
const bigInt = 1234567890123456789012345678901234567890n;
console.log(bigInt); // Output: 1234567890123456789012345678901234567890n
```

#### Dynamic imports

This is a new mechanism for the dynamic import of modules in JavaScript. Previously, importing modules was done statically in the source code. With the introduction of dynamic import(), it is possible to load modules asynchronously at runtime.

```javascript 
async function loadModule() {
  const module = await import('./module.js');
  console.log(module.default);
}
```



### ECMAScript 2021 (ES2021):

#### String.prototype.matchAll

This method returns an iterator that yields all the matches of a regular expression in a string.

```javascript 
const str = 'Hello, world!';
const regex = /\w+/g;

const matches = Array.from(str.matchAll(regex));
console.log(matches);
// [["Hello"], ["world"]]
```

#### Numeric separators

This feature allows for using underscores as separators in numeric literals, making it easier to read and write large numbers.

```javascript 
const x = 1_000_000;
console.log(x); // 1000000
```

#### Logical assignment operators

These operators provide a shorthand for performing logical operations, such as `and` and `or`, and then assigning the result to a variable.

```javascript 
let x = 42;
x ||= 23;
console.log(x); // 42

x &&= 23;
console.log(x); // 23
```


