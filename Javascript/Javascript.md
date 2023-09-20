# Objects

Objects can be created with object literals, with the new keyword, and with the Object.create()

# Prototypes

Almost every JavaScript object has a second JavaScript object associated with it. This second object is known as a prototype, and the first object inherits properties from the prototype.

So the object created by `new Object()` inherits from Object.prototype, just as the object created by `{}` does. Similarly, the object created by `new Array()` uses Array.prototype as its prototype, and the object created by` new Date()` uses Date.prototype as its prototype. This can be confusing when first learning JavaScript. Remember: almost all objects have a prototype, but only a relatively small number of objects”have a prototype property. It is these objects with prototype properties that define the prototypes for all the other objects.

`Object.prototype` is one of the rare objects that has no prototype: it does not inherit any properties. Other prototype objects are normal objects that do have a prototype. Most built-in constructors (and most user-defined constructors) have a prototype that inherits from
Object.prototype

## Object.create()

Object.create() creates a new object, using its first argument as
the prototype of that object:”

```javascript

“let o1 = Object.create({x: 1, y: 2});     // o1 inherits properties x and y.
o1.x + o1.y   ”

```

	You can pass null to create a new object that does not have a
	prototype, but if you do this, the newly created object will not
	inherit anything, not even basic methods like toString() (which
	means it won’t work with the + operator either)

```js
“let o2 = Object.create(null);             // o2 inherits no props or methods.”
```

“If you want to create an ordinary empty object (like the object returned by =={} or new Object()==), pass Object.prototype:

```js
let o3 = Object.create(Object.prototype); // o3 is like {} or new Object().”
```

One use for Object.create() is when you want to guard against
unintended (but nonmalicious) modification of an object by a library
function that you don’t have control over. Instead of passing the
object directly to the function, you can pass an object that inherits
from it. 

# Inheritance

JavaScript objects have a set of “own properties,” and they also
inherit a set of properties from their prototype object.

https://dev.to/lydiahallie/javascript-visualized-prototypal-inheritance-47co
![[Javascript/assets/59nlnyqioosaowj09xn8.gif]]

## Deleting Properties

```js
“delete book.author;          // The book object now has no author property.
delete book["main title"];   // Now it doesn't have "main title", either.”
```

A delete expression evaluates to true if the delete succeeded or if the delete had no effect (such as deleting a nonexistent property). delete also evaluates to true when used (meaninglessly) with an expression that is not a property access expression:”

```js
let o = {x: 1};    // o has own property x and inherits property toString
delete o.x         // => true: deletes property x
delete o.x         // => true: does nothing (x doesn't exist) but true anyway
delete o.toString  // => true: does nothing (toString isn't an own property)
delete 1           // => true: nonsense, but true anyway
```

delete does not remove properties that have a configurable attribute of false. Certain properties of built-in objects are non-configurable, as are properties of the global object created by variable declaration and function declaration. In strict mode, attempting to delete a non-configurable property causes a TypeError. In non-strict mode, delete simply evaluates to false in this case:

```js
// In strict mode, all these deletions throw TypeError instead of returning false
delete Object.prototype // => false: property is non-configurable
var x = 1;              // Declare a global variable
delete globalThis.x     // => false: can't delete this property
function f() {}         // Declare a global function
delete globalThis.f     // => false: can't delete this property either”
```



## Spread Operator
In ES2018 and later, you can copy the properties of an existing object into a new object using the “spread operator” ... inside an object literal:

```js
let position = { x: 0, y: 0 };
let dimensions = { width: 100, height: 75 };
let rect = { ...position, ...dimensions };
rect.x + rect.y + rect.width + rect.height // => 175

```
If the object that is spread and the object it is being spread into both have a property with the same name, then the value of that property will be the one that comes last:

```js
let o = { x: 1 };
let p = { x: 0, ...o };
p.x   // => 1: the value from object o overrides the initial value
let q = { ...o, x: 2 };
q.x   // => 2: the value 2 overrides the previous value from o.
```

**Also note that the spread operator only spreads the own properties of
an object, not any inherited ones:**

```js
let o = Object.create({x: 1}); // o inherits the property x
let p = { ...o };
p.x                            // => undefined

```

## [Object.keys, values, entries](https://javascript.info/keys-values-entries#object-keys-values-entries)

For plain objects, the following methods are available:

- [Object.keys(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) – returns an array of keys.
- [Object.values(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values) – returns an array of values.
- [Object.entries(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) – returns an array of `[key, value]` pairs.
https://javascript.info/keys-values-entries


# Array

Creating Arrays: The Array.of() and Array.from() Factory Methods

### Array.of()

In JavaScript, the `Array()` constructor function has a quirk: when invoked with a single numeric argument, it interprets that argument as the desired array length. However, if it's invoked with more than one numeric argument, it treats those arguments as elements to be included in the array. This poses a problem when you want to create an array with just a single numeric element.

To address this limitation, ES6 introduced the `Array.of()` function. `Array.of()` is a factory method that creates and returns a new array, using its arguments as elements, regardless of how many there are:

```javascript
Array.of();          // Returns an empty array with no arguments
Array.of(10);        // Creates an array with a single numeric argument: [10]
Array.of(1, 2, 3);   // Creates an array with multiple numeric arguments: [1, 2, 3]
```

### Array.from()

Another array factory method introduced in ES6 is `Array.from()`. This method expects an iterable or array-like object as its first argument and returns a new array containing the elements of that object. When used with an iterable argument, `Array.from(iterable)` behaves similarly to the spread operator `[...iterable]`. It's also a straightforward way to create a copy of an array:

```javascript
let copy = Array.from(original); // Creates a copy of 'original' array
```

`Array.from()` is especially valuable because it defines a means to make a true-array copy of an array-like object. Array-like objects are non-array objects that have a numeric `length` property and store values with properties whose names happen to be integers.

### Sparse Arrays

A sparse array is an array where the elements do not have contiguous indexes starting at 0. Normally, the `length` property of an array specifies the number of elements it contains. In sparse arrays, the value of the `length` property is greater than the actual number of elements.

Sparse arrays can be created in different ways. You can use the `Array()` constructor with a specified length to create a sparse array:

```javascript
let a = new Array(5);   // Creates an array with no elements, but 'a.length' is 5.
```

Alternatively, you can create an empty array with length 0 by simply assigning an empty array literal:

```javascript
a = [];                 // Creates an array with no elements and length = 0.
```

Sparse arrays can also be created by assigning a value to an array index that is larger than the current array length:

```javascript
a[1000] = 0;            // Adds one element but sets the length to 1001.
```

These mechanisms allow you to work with arrays that have non-contiguous indexes, which can be useful in specific situations.

In JavaScript, `map`, `filter`, and `reduce` are higher-order functions that operate on arrays. They allow you to perform various transformations and operations on arrays in a concise and functional way. Here's an explanation of each of these functions with examples:

1. **`map`**

   The `map` function applies a given function to each element of an array and returns a new array containing the results of those function calls. It doesn't modify the original array.

   ```javascript
   const numbers = [1, 2, 3, 4, 5];

   const squaredNumbers = numbers.map((num) => num ** 2);

   console.log(squaredNumbers); // Output: [1, 4, 9, 16, 25]
   ```

   In this example, we use `map` to square each number in the `numbers` array, creating a new array (`squaredNumbers`) with the squared values.

2. **`filter`**

   The `filter` function creates a new array containing all elements from the original array that satisfy a specified condition. It also doesn't modify the original array.

   ```javascript
   const numbers = [1, 2, 3, 4, 5];

   const evenNumbers = numbers.filter((num) => num % 2 === 0);

   console.log(evenNumbers); // Output: [2, 4]
   ```

   Here, `filter` is used to create a new array (`evenNumbers`) that contains only the even numbers from the `numbers` array.

3. **`reduce`**

   The `reduce` function is used to accumulate or combine the elements of an array into a single value. It iterates through the array and applies a function that accumulates the result as it goes along.

   ```javascript
   const numbers = [1, 2, 3, 4, 5];

   const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0 /* initialValue */);

   console.log(sum); // Output: 15
   ```

   In this example, `reduce` is used to calculate the sum of all numbers in the `numbers` array. The `0` passed as the second argument to `reduce` initializes the `accumulator`.


## # `slice()`, `concat()`, and `splice()` 
1. **`slice()`**:

   The `slice()` method creates a shallow copy of a portion of an array into a new array. It doesn't modify the original array; instead, it returns a new array containing the selected elements. `slice()` accepts one or two arguments:

   - `start` (optional): The index at which to start extracting elements (inclusive). If omitted, it starts from index 0.
   - `end` (optional): The index at which to stop extracting elements (exclusive). If omitted, it extracts until the end of the array.

   ```javascript
   const fruits = ["apple", "banana", "cherry", "date", "fig"];

   const slicedFruits = fruits.slice(1, 4);
   console.log(slicedFruits); // Output: ["banana", "cherry", "date"]
   ```

   In this example, `slice(1, 4)` extracts elements from index 1 (inclusive) to 4 (exclusive), creating a new array.

2. **`concat()`**:

   The `concat()` method is used to merge two or more arrays, creating a new array without modifying the original arrays. It takes one or more arrays or values as arguments and returns a new array that includes the elements from all the arrays passed to it.

   ```javascript
   const arr1 = [1, 2];
   const arr2 = [3, 4];
   const arr3 = [5, 6];

   const mergedArray = arr1.concat(arr2, arr3);
   console.log(mergedArray); // Output: [1, 2, 3, 4, 5, 6]
   ```

   In this example, `concat()` is used to merge `arr1`, `arr2`, and `arr3` into a new array.

3. **`splice()`**:

   The `splice()` method is used to change the contents of an array by removing, replacing, or adding elements. It directly modifies the original array and returns an array containing the removed elements. `splice()` takes three arguments:

   - `start`: The index at which to start changing the array.
   - `deleteCount` (optional): The number of elements to remove from the `start` index. If set to 0, no elements are removed.
   - `item1, item2, ...` (optional): Elements to add to the array at the `start` index.

   ```javascript
   const numbers = [1, 2, 3, 4, 5];

   const removedElements = numbers.splice(1, 2, 6, 7);
   console.log(numbers); // Output: [1, 6, 7, 4, 5]
   console.log(removedElements); // Output: [2, 3]
   ```

   In this example, `splice(1, 2, 6, 7)` removes two elements starting from index 1 and replaces them with `6` and `7`, resulting in the modified `numbers` array.

These array methods provide different ways to manipulate arrays in JavaScript, allowing you to extract, merge, or modify elements to suit your specific needs while maintaining the original data intact when necessary.


# Asynchronous JavaScript

## What is a Callback Function?

A callback is a function that you write and then pass to some other function. That other function then invokes (“calls back”) your function when some condition is met or some (asynchronous) event occurs.”


# Promise
**Promises** are the foundation of asynchronous programming in modern JavaScript. A promise is an object returned by an asynchronous function, which represents the current state of the operation. At the time the promise is returned to the caller, the operation often isn't finished, but the promise object provides methods to handle the eventual success or failure of the operation.
![[promise.png]]

### How to Consume Promises

```javascript
const request = fetch('https://course-api.com/react-store-products').then((response) =>{
    console.log(response);
    return response.json()
}).then((data) =>{
    console.log(data);
})
```
We make a request to the country API. Then, after the fetch request, we use the `then()` method to consume the promise.

## How to Handle Rejected Promises

```javascript
function call(){

    const request = fetch('https://course-api.com/react-store-products').then((response) =>{
        console.log(response);
        return response.json()
    }).then((data) =>{
        console.log(data);
    }).catch((err) =>{
        alert(err);
    })

}
```
Now the `catch()` method will get an error from the rejected promise and will display the message in an alert.
Along with the catch() method, there is one more helpful method called `finally()`


## How to Create a Promise
https://javascript.info/promise-basics
The constructor syntax for a promise object is:

```js
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
```

	When you create a `new Promise` using the Promise constructor, you pass in a function that takes two arguments: `resolve` and `reject`. These are callback functions that you, as the developer, will call to indicate the outcome of the asynchronous operation.

![[promise constructor.png]]
# Async/Await
https://dev.to/lydiahallie/javascript-visualized-promises-async-await-5gke
```js
async function(){
//waits for promise to resolve
let resolvedPromise = await new Promise(...){....};
//execution is stopped util promise is resolved

return resolvedPromise;
}
```
![[e5duygomitj9o455107a.gif]]

![[promise pending.png]]![[promise fulfill.png]]


