
# Data types

| Type                                                                                                | `typeof` return value | Object wrapper                                                                                        |
| --------------------------------------------------------------------------------------------------- | --------------------- | ----------------------------------------------------------------------------------------------------- |
| [Null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#null_type)           | `"object"`            | N/A                                                                                                   |
| [Undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#undefined_type) | `"undefined"`         | N/A                                                                                                   |
| [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#boolean_type)     | `"boolean"`           | [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) |
| [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#number_type)       | `"number"`            | [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)   |
| [BigInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#bigint_type)       | `"bigint"`            | [`BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)   |
| [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#string_type)       | `"string"`            | [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)   |
| [Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#symbol_type)       | `"symbol"`            | [`Symbol`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)   |
## [Interpreted vs compiled code](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript#interpreted_versus_compiled_code)
## Scripted vs Compiled Languages

- **Scripted Languages**: The source code is interpreted at runtime, with the interpreter processing the code line by line as the program runs.
- **Compiled Languages**: The source code is translated into machine code or an intermediate code before runtime, and the resulting executable is run independently.

JavaScript is a programming language, not just a scripting language. However, confusion might arise due to historical reasons and the way JavaScript is often used in web development.


# Execution in JS
### creation phase
sets up global context 
assigns memory for variable
### execution phase
It starts going through the entire code line by line from top to bottom and execute the code


# Lexical Environment

A lexical environment is **a data structure that stores the variables and functions that are defined in the current scope and all of the outer scopes**

For example, consider the following snippet:

```
var a = 20;
var b = 40;

function foo() {
  console.log('bar');
}
```

So the lexical environment for the above snippet looks like this:

```
lexicalEnvironment = {
  a: 20,
  b: 40,
  foo: <ref. to foo function>
}
```

# `undefined` vs `not defined`

**`undefined` indicates that a variable has been declared but not given a value, while `not defined` indicates that a variable does not exist**

# Hoisting

interpreter move the _declaration_ of functions, variables, classes, or imports to the top of their scope, prior to execution of the code.

When working with `var` and `function` declarations, they are stored in the variable object in memory, allowing them to be accessed even before their explicit declaration in the code.
 
<aside><font color="#c0504d"> `var` has a function context</font></aside>

This means that you can use a function or variable in your code even before it's declared.

```jsx
console.log(x);
console.log(getName());

var x = 2;
function getName() {
    return "hello world";
}
```

```jsx
undefined
hello world
```

Note: `var` is allocated memory with inital val as `undefined` actual val is assigned when interpreter reaches the statement

However, it's important to note that when using `let` and `const`, the hoisting behavior is different. While the declarations are still hoisted, accessing the variables before their declaration results in a `ReferenceError`. This is because variables declared with `let` and `const` are in a **temporal dead zone** until the actual declaration is encountered during the runtime.

<aside> 💡 `let` and `const` are block-scoped, whereas `var` is function-scoped.

</aside>

# types of error
Reference error
Syntax error
Types error

# Block

A block in JavaScript is a set of statements that are executed together. It is defined by curly braces { }.

## Closures

A closure is a function that has access to the parent scope, even after the parent function has closed.

JS will automatically store the **state of a closure in the heap memory**, even after the parent function has returned.

This behavior makes them useful for encapsulating private variables.

```jsx
function encapsulatedState(x) {
  let state = 10;
  return function() {
    state += x;
    return state;
  }
```

# First-class Function

A programming language is said to have **First-class functions** when functions in that language are treated like any other variable.

```jsx
const foo = () => {
  console.log("foobar");
};
foo(); // Invoke it using the variable
// foobar
```


# **Callback Functions**

[What is a Callback Function in JavaScript?](https://www.freecodecamp.org/news/what-is-a-callback-function-in-javascript/)

A **callback function** is a function that is passed _as an argument_ to another function, to be “called back” at a later time.

A function that accepts other functions as arguments is called a **higher-order function**, which contains the logic for _when_ the callback function gets executed.

```jsx
function createQuote(quote, callback){ 
  var myQuote = "Like I always say, " + quote;
  callback(myQuote); // 2
}

function logQuote(quote){
  console.log(quote);
}

createQuote("eat your vegetables!", logQuote); // 1

// Result in console: 
// Like I always say, eat your vegetables!
```

# Function expression vs declaration vs statement???
# Event loop

[https://dev.to/nodedoctors/an-animated-guide-to-nodejs-event-loop-3g62](https://dev.to/nodedoctors/an-animated-guide-to-nodejs-event-loop-3g62)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/1f74e2bb-077f-4ca5-b5fd-0418784e10e7/Untitled.png)

- JavaScript is a **single-threaded programming language**. This means that JavaScript can do only one thing at a single point in time.
- JavaScript offloads asynchronous tasks to its environment (browser or Node.js).
- Environments are equipped to handle asynchronous tasks concurrently.

**Microtask Queue:**

- Higher precedence than the callback queue.
- Primarily for Promise callbacks and `process.nextTick`.
- Executes before the callback queue in the event loop.

**Callback Queue:**

- Lower precedence compared to the microtask queue.
- Includes tasks scheduled by `setTimeout`, `setInterval`, and I/O events.
- Executed after the microtask queue in the event loop.

![3e9d52bc38fa287a4cf10dcf8139076d.gif](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/d1b0f253-683f-4aea-b373-fa35c10b4e89/3e9d52bc38fa287a4cf10dcf8139076d.gif)


# call apply and bind

[Learn & Solve : call(), apply() and bind() methods in JavaScript](https://www.codingame.com/playgrounds/9799/learn-solve-call-apply-and-bind-methods-in-javascript)

1. “this” always refers to an object.
2. “this” refers to an object which calls the function it contains.
3. In the global context “this” refers to either window object or is undefined if the ‘strict mode’ is used.

```jsx
var car = {
    registrationNumber: "GA12345",
    brand: "Toyota",

    displayDetails: function(){
        console.log(this.registrationNumber + " " + this.brand);
    }
}
```

The above will work perfectly fine as long as we use it this way:

```jsx
car.displayDetails(); // GA12345 Toyota
```

But what if we want to borrow a method?

```jsx
var myCarDetails =  car.displayDetails;
myCarDetails();
```

Well, this won’t work as the “this” will be now assigned to the global context which doesn’t have neither the registrationNumber nor the brand property.

# The bind() Method

For such cases we can use the ECMAScript 5 bind() method of the Function.prototype property. This means bind() can be used by every single function.

```jsx
var myCarDetails = car.displayDetails.bind(car);
myCarDetails(); // GA12345 Toyota
```

The bind() method creates a new function where “this” refers to the parameter in the parenthesis in the above case “car”. This way the bind() method enables calling a function with a specified “this” value.

What if we would like to pass a parameter to the displayDetails function? We can use the bind method again. The following argument of the bind() method will provide an argument to the function bind() is called on.

Let me rewrite the car object:

```jsx
var car = {
    registrationNumber: "GA12345",
    brand: "Toyota",

    displayDetails: function(ownerName){
        console.log(ownerName + ", this is your car: " + this.registrationNumber + " " + this.brand);
    }
}
```

Example of passing arguments with bind():

```jsx
var myCarDetails = car.displayDetails.bind(car, "Vivian"); // Vivian, this is your car: GA12345 Toyota
```

### **call() and apply() methods**

Similar but slightly different usage provide the call() and apply() methods which also belong to the Function.prototype property.

This time there is a car object without the displayDetails function, which is located in the global context.

```jsx
var car = {
    registrationNumber: "GA12345",
    brand: "Toyota"
}

function displayDetails(ownerName) {
    console.log(ownerName + ", this is your car: " + this.registrationNumber + " " + this.brand);
}

```

We can use the apply() function:

```jsx
displayDetails.apply(car, ["Vivian"]); // Vivian, this is your car: GA12345 Toyota
```

Or

```jsx
displayDetails.call(car, "Vivian"); // Vivian, this is your car: GA12345 Toyota

```

Note that when using the apply() function the parameter must be placed in an array. Call() accepts both an array of parameters and a parameter itself. Both are great tools for borrowing functions in JavaScript.

bind(), call() and apply() functions can make your life easier when you need to set the value of ‘this’. Hope the post was helpful.

**JavaScript Debounce vs. Throttle**

[https://www.vehidtrtak.com/blog/javascript-debounce-and-throttle-explained](https://www.vehidtrtak.com/blog/javascript-debounce-and-throttle-explained)

# Debounce And Throttle
https://youtu.be/cjIswDCKgu0

https://stackoverflow.com/a/25991510/21329968
- **Throttling** will delay executing a function. It will reduce the notifications of an event that fires multiple times.
- **Debouncing** will bunch a series of sequential calls to a function into a single call to that function. It ensures that one notification is made for an event that fires multiple times.
You can visually see the difference [here](https://web.archive.org/web/20220117092326/http://demo.nimius.net/debounce_throttle/)

If you have a function that gets called a lot - for example when a resize or mouse move event occurs, it can be called a lot of times. If you don't want this behaviour, you can **Throttle** it so that the function is called at regular intervals. **Debouncing** will mean it is called at the end (or start) of a bunch of events.

## **debounce**

```jsx
function debouncer(callback, delay = 1000) {
    let time;

    return function () {
        clearTimeout(time);
        console.log("Debouncer called");

        time = setTimeout(() => {
            callback();
            console.log("Callback invoked");
        }, delay);
    };
}
```

## **throttle**

```jsx
function throttle(callback, delay = 1000) {
    let shouldWait = false;

    return function () {
        console.log("Throttle called");

        if (!shouldWait) {
            shouldWait = true;
            callback();
            console.log("Callback invoked");

            setTimeout(() => (shouldWait = false), delay);
        }
    };
}
```

# **currying**

```jsx
function sum(a, b, c) {
    return a + b + c;
}
sum(1,2,3); // 6
```

```coffeescript
function sum(a) {
    return (b) => {
        return (c) => {
            return a + b + c
        }
    }
}
console.log(sum(1)(2)(3)) // 6
```

practical application???




# Promise
 A _Promise_ is an object representing the eventual completion or failure of an asynchronous operation

<svg xmlns="http://www.w3.org/2000/svg" width="512" height="246" viewBox="0 0 512 246"><defs><style>@import url(https://fonts.googleapis.com/css?family=Open+Sans:bold,italic,bolditalic%7CPT+Mono);@font-face{font-family:&apos;PT Mono&apos;;font-weight:700;font-style:normal;src:local(&apos;PT MonoBold&apos;),url(/font/PTMonoBold.woff2) format(&apos;woff2&apos;),url(/font/PTMonoBold.woff) format(&apos;woff&apos;),url(/font/PTMonoBold.ttf) format(&apos;truetype&apos;)}</style></defs><g id="promise" fill="none" fill-rule="evenodd" stroke="none" stroke-width="1"><g id="promise-resolve-reject.svg"><path id="Rectangle-1" fill="#FBF2EC" stroke="#DBAF88" stroke-width="2" d="M1 91h182v70H1z"/><text id="new-Promise(executor" fill="#7E7C7B" font-family="PTMono-Regular, PT Mono" font-size="14" font-weight="normal"><tspan x="2" y="82">new Promise(executor)</tspan></text><text id="state:-&quot;pending&quot;-res" fill="#AF6E24" font-family="PTMono-Regular, PT Mono" font-size="14" font-weight="normal"><tspan x="13" y="115.432">state: &quot;pending&quot;</tspan> <tspan x="13" y="135.432">result: undefined</tspan></text><path id="Line" fill="#C06334" fill-rule="nonzero" d="M196.51 134.673l.908.419 103.284 47.574 2.51-5.45L313 189.433l-15.644.5 2.509-5.45-103.283-47.574-.909-.418.837-1.817z"/><path id="Line-Copy" fill="#C06334" fill-rule="nonzero" d="M297.38 56L313 57l-10.173 11.896-2.335-5.528-103.103 43.553-.921.39-.778-1.843.92-.39 103.104-43.552-2.334-5.527z"/><text id="resolve(value)" fill="#C06334" font-family="PTMono-Regular, PT Mono" font-size="14" font-weight="normal" transform="rotate(-23 244.39 72.63)"><tspan x="185.59" y="77.13">resolve(value)</tspan></text><text id="reject(error)" fill="#C06334" font-family="PTMono-Regular, PT Mono" font-size="14" font-weight="normal" transform="rotate(25 251.634 150.64)"><tspan x="197.034" y="155.141">reject(error)</tspan></text><path id="Rectangle-1-Copy" fill="#FBF2EC" stroke="#478964" stroke-width="2" d="M323 10h182v64H323z"/><text id="state:-&quot;fulfilled&quot;-r" fill="#478964" font-family="PTMono-Regular, PT Mono" font-size="14" font-weight="normal"><tspan x="338" y="34.432">state: &quot;fulfilled&quot;</tspan> <tspan x="338" y="54.432">result: value</tspan></text><path id="Rectangle-1-Copy-3" fill="#FEF1F0" stroke="#D35155" stroke-width="2" d="M323 177h182v64H323z"/><text id="state:-&quot;rejected&quot;-re" fill="#AF6E24" font-family="PTMono-Regular, PT Mono" font-size="14" font-weight="normal"><tspan x="338" y="201.432">state: &quot;rejected&quot;</tspan> <tspan x="338" y="221.432">result: error</tspan></text></g></g></svg>

```js
let promise = new Promise(function(resolve, reject) {
  // the function is executed automatically when the promise is constructed

  // after 1 second signal that the job is done with the result "done"
  setTimeout(() => resolve("done"), 1000);
});

```

### Common Promise utility methods:

[Promise API](https://javascript.info/promise-api)
### `Promise.all(iterable)`:
    
    - Resolves when **all** Promises in the iterable resolve successfully.
    - If any promise is rejected, the entire `Promise.all` operation fails immediately.
	
### `Promise.allSettled(iterable)`:
    - Waits for **all** promises to settle (resolve or reject), regardless of the result.
    - The resulting array contains objects with two properties:
        - `{status: "fulfilled", value: result}` for successful responses.
        - `{status: "rejected", reason: error}` for errors.
		
### `Promise.race(iterable)`:
    - Waits for the **first** settled promise (either resolved or rejected) within the iterable.
	
### `Promise.any(iterable)`:
    - Waits for the **first successful** promise to resolve.
    - If all promises are rejected, it’s rejected with an `AggregateError`.




## **Async/Await**??

https://dev.to/lydiahallie/javascript-visualized-promises-async-await-5gke

[⭐️🎀 JavaScript Visualized: Promises & Async/Await](https://dev.to/lydiahallie/javascript-visualized-promises-async-await-5gke)

```jsx
async function(){
//waits for promise to resolve
let resolvedPromise = await new Promise(...){....};
//execution is stopped util promise is resolved

return resolvedPromise;
}
```

![e5duygomitj9o455107a.gif](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/67cd0d95-6072-45ad-8f5f-ebd3d39878ee/e5duygomitj9o455107a.gif)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/7a9c7826-c918-46ab-a599-8b111b1d4dde/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/a78dc735-0ca7-40b9-8505-56a27ce167ce/Untitled.png)






## Closures
A closure is _a function having access to the parent scope_, even after the parent function has closed
![[closures.png]]


# Immediately Invoked Function Expressions (IIFE)

```js
(
		async	funtion(){
	 //...write code here
		}
)()
```


```js
(function () {
  // …
})();

(() => {
  // …
})();

(async () => {
  // …
})();

```


## imp question ??


# [What is event bubbling and capturing?](https://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing)

[Event Bubbling in JavaScript – How Event Propagation Works with Examples](https://www.freecodecamp.org/news/event-bubbling-in-javascript/)

https://stackoverflow.com/a/4616720/21329968

Event bubbling and capturing are two ways of event propagation in the HTML DOM API, when an event occurs in an element inside another element, and both elements have registered a handle for that event. The event propagation mode determines in [which order the elements receive the event](http://www.quirksmode.org/js/events_order.html).

With bubbling, the event is first captured and handled by the innermost element and then propagated to outer elements.

With capturing, the event is first captured by the outermost element and propagated to the inner elements.

Capturing is also called "trickling", which helps remember the propagation order:

> trickle down, bubble up


![[Pasted image 20230921021019.png]](https://stackoverflow.com/a/67346472/21329968)


https://stackoverflow.com/a/30233082/21329968
I have found this [tutorial at javascript.info](http://javascript.info/tutorial/bubbling-and-capturing) to be very clear in explaining this topic. And its 3-points summary at the end is really talking to the crucial points. I quote it here:

1. Events first are captured down to deepest target, then bubble up. In IE<9 they only bubble.
2. All handlers work on bubbling stage excepts `addEventListener` with last argument `true`, which is the only way to catch the event on capturing stage.
3. Bubbling/capturing can be stopped by `event.cancelBubble=true` (IE) or `event.stopPropagation()` for other browsers.
## Event delegation

event delegation is a pattern that efficiently handles events

In JavaScript, if you have a large number of [event handlers](https://www.javascripttutorial.net/javascript-dom/handling-events-in-javascript/) on a page, these event handlers will directly impact the performance because of the following reasons:

- First, each event handler is a [function](https://www.javascripttutorial.net/javascript-function/) which is also an [object](https://www.javascripttutorial.net/javascript-objects/) that takes up memory. The more objects in the memory, the slower the performance.
- Second, it takes time to assign all the event handlers, which causes a delay in the interactivity of the page.

To solve this issue, you can leverage the [event bubbling](https://www.javascripttutorial.net/javascript-dom/javascript-events/).

```jsx
let home = document.querySelector('#home');
home.addEventListener('click',(event) => {
    console.log('Home menu item was clicked');
});

let dashboard = document.querySelector('#dashboard');
dashboard.addEventListener('click',(event) => {
    console.log('Dashboard menu item was clicked');
});

let report = document.querySelector('#report');
report.addEventListener('click',(event) => {
    console.log('Report menu item was clicked');
});
```

```jsx
let menu = document.querySelector('#menu');

menu.addEventListener('click', (event) => {
    let target = event.target;

    switch(target.id) {
        case 'home':
            console.log('Home menu item was clicked');
            break;
        case 'dashboard':
            console.log('Dashboard menu item was clicked');
            break;
        case 'report':
            console.log('Report menu item was clicked');
            break;
    }
});
```


1. **What is ES6, and why was it introduced?**
    
    - ES6, or ECMAScript 2015, is the sixth edition of the ECMAScript standard, which is the scripting language specification that JavaScript is based on. It was introduced to enhance the language's capabilities, introduce new features, and improve developer productivity.
    - Some key features include:
        - `let` and `const` for variable declarations
        - Arrow functions
        - Template literals `hello world ${state}`
        - Destructuring assignment
        - Classes
        - Promises for handling asynchronous operations
2. A**rrow functions**
    
    - Arrow functions are a concise way to write function expressions in JavaScript.
    - They have a shorter syntax, do not bind their own `this`, and do not have their own `arguments` object.
    
    [Why can't I access `this` within an arrow function?](https://stackoverflow.com/a/34208235/21329968)
    
    [Arrow functions perform _lexical binding_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) and uses the surrounding scope as the scope of `this`. For example, imagine (for some weird reason) you define `Cat` inside of a `Dog` constructor.
    
    ```jsx
    function Dog() {
      // do dog like things
      function Cat() { ... }
      Cat.prototype.sound = () => {
        // this == instance of Dog!
      };
    }
    ```
    
    So whatever the _surrounding_ scope is becomes the scope of an arrow function.
    

prototype??











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
![[59nlnyqioosaowj09xn8.gif]]

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


# function declaration vs expression
[Function Declaration vs Function Expression (freecodecamp.org)](https://www.freecodecamp.org/news/function-declaration-vs-function-expression/)