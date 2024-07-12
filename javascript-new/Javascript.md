## [Interpreted vs compiled code](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript#interpreted_versus_compiled_code)

compiled -> machine code -> runtime

You might hear the terms interpreted and compiled in the context of programming. In interpreted languages, the code is run from top to bottom and the result of running the code is immediately returned. You don't have to transform the code into a different form before the browser runs it. The code is received in its programmer-friendly text form and processed directly from that.

Compiled languages on the other hand are transformed (compiled) into another form before they are run by the computer. For example, C/C++ are compiled into machine code that is then run by the computer. The program is executed from a binary format, which was generated from the original program source code.

JavaScript is a lightweight interpreted programming language. The web browser receives the JavaScript code in its original text form and runs the script from that. From a technical standpoint, most modern JavaScript interpreters actually use a technique called just-in-time compiling to improve performance; the JavaScript source code gets compiled into a faster, binary format while the script is being used, so that it can be run as quickly as possible. However, JavaScript is still considered an interpreted language, since the compilation is handled at run time, rather than ahead of time.

## Scripted vs Compiled Languages

- **Scripted Languages**: The source code is interpreted at runtime, with the interpreter processing the code line by line as the program runs.
- **Compiled Languages**: The source code is translated into machine code or an intermediate code before runtime, and the resulting executable is run independently.

JavaScript is a programming language, not just a scripting language. However, confusion might arise due to historical reasons and the way JavaScript is often used in web development.

When JavaScript was first introduced by Netscape in the mid-1990s, it was primarily used for client-side scripting within web browsers. It was initially designed to add interactivity and dynamic behavior to web pages. At that time, many people referred to it as a "scripting language" because it was often embedded in HTML documents and executed on the client side.

Over the years, JavaScript evolved and expanded its capabilities. With the introduction of Node.js, developers gained the ability to run JavaScript on server-side environments, enabling them to build full-stack applications. As a result, JavaScript transitioned from being primarily a client-side scripting language to a versatile programming language that can be used for both front-end and back-end development.

Despite its programming capabilities, the historical association with client-side scripting and its initial use on the web may lead to the misconception that JavaScript is only a scripting language. In reality, it is a fully-fledged programming language that supports both procedural and object-oriented programming paradigms.

Execution in JS

### creation phase

| Variable Object (Memory) | Code |
| ------------------------ | ---- |
| x = undefined            |      |

getName() {     return "hello world"; } | console.log(x); console.log(getName());

var x = 2; function getName() {     return "hello world"; } |

### execution phase

<aside> 💡

when using `var` memory is assigned to var but initially value is set to `undefined`. When interpreter reaches the line `var x = 2;` **then only val is assigned**

but function works normally

</aside>

[https://lh7-us.googleusercontent.com/bVe2RG_Txdj4TqK7LyLggLryR8eiebC-KWA2i_9Q13GiRGhZER2QALRmN2-6fu4wqmuSqCQXYOIrzafFiJ5PNkkBAgCahIU7r_iIvHUwJIsecWseT6HwkalO7a7xWcM9xcgQg4YzddAIP5s1o4ibXiw](https://lh7-us.googleusercontent.com/bVe2RG_Txdj4TqK7LyLggLryR8eiebC-KWA2i_9Q13GiRGhZER2QALRmN2-6fu4wqmuSqCQXYOIrzafFiJ5PNkkBAgCahIU7r_iIvHUwJIsecWseT6HwkalO7a7xWcM9xcgQg4YzddAIP5s1o4ibXiw)

**Execution Stack**

```jsx
let a = 'Hello World!';
function first() {
  console.log('Inside first function');
  second();
  console.log('Again inside first function');
}
function second() {
  console.log('Inside second function');
}
first();
console.log('Inside Global Execution Context');
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/cf19f9dc-76fb-436f-a04d-87e59c463607/Untitled.png)

**Lexical Environment**

A _lexical environment_ is a structure that holds **identifier-variable mapping**. (here **identifier** refers to the name of variables/functions, and the **variable** is the reference to actual object [including function object and array object] or primitive value).

For example, consider the following snippet:

```
var a = 20;
var b = 40;function foo() {
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

JavaScript **Hoisting** refers to the process whereby the interpreter appears to move the _declaration_ of functions, variables, classes, or imports to the top of their scope, prior to execution of the code.

When working with `var` and `function` declarations, they are stored in the variable object in memory, allowing them to be accessed even before their explicit declaration in the code.

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

However, it's important to note that when using `let` and `const`, the hoisting behavior is different. While the declarations are still hoisted, accessing the variables before their declaration results in a `ReferenceError`. This is because variables declared with `let` and `const` are in a "temporal dead zone" until the actual declaration is encountered during the runtime.

In summary, hoisting in JavaScript facilitates the availability of certain declarations before their appearance in the code, but the behavior varies based on the type of declaration and the use of `var`, `let`, or `const`.

```jsx
console.log(x);
let x = 2;
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/bbb16a1f-d009-45fa-a008-5eacf59cc78c/Untitled.png)

<aside> 💡 `let` and `const` are block-scoped, whereas `var` is function-scoped.

</aside>

# types of error

[Oh, no, errors! (And how to deal with them) / Programming fundamentals](https://hexlet.io/courses/intro_to_programming/lessons/errors/theory_unit)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/f03794f2-533c-48eb-ba49-6a74dd58534f/Untitled.png)

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

# Function expression vs declaration vs statement???

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

# Higher order function

functions that take one or more functions as arguments, or return a function as their result.

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

**debounce**

![js-debounce.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/fe505bc4-830e-4e2c-a0a7-0fdb36ac296e/js-debounce.png)

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

**throttle**

![js-throttle.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/22095443-9873-445f-821c-217be0795df7/js-throttle.png)

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

# Event bubbling , capture

[Event Bubbling in JavaScript – How Event Propagation Works with Examples](https://www.freecodecamp.org/news/event-bubbling-in-javascript/)

# Event delegation

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

## **Promise**

Promises are used to handle asynchronous operations, such as making network requests or reading files, in a more organized and manageable way. Promises are designed to represent the eventual result (or failure) of an asynchronous operation.

**When you create a new Promise using the `Promise` constructor, you pass in a function that takes two arguments: `resolve` and `reject`. These are callback functions that you, as the developer, will call to indicate the outcome of the asynchronous operation.**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/d9a2cf0c-8868-41c9-bfa6-41fe05c3a49f/Untitled.png)

> **function must be passed with parameter: resolve , reject**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/e769adc3-ec44-4ab7-96a0-7df7cd23ff36/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7dee642d-64f1-4400-92a3-4b0fa7d3685a/abae232e-ff0f-4984-92a3-8423ddb87ea9/Untitled.png)

```jsx
// the execution: catch -> then
new Promise((resolve, reject) => {

  throw new Error("Whoops!");

}).catch(function(error) {

  alert("The error is handled, continue normally");

}).then(() => alert("Next successful handler runs"));
```

```jsx
new Promise((resolve, reject) => {
  resolve("ok");
}).then((result) => {
  throw new Error("Whoops!"); // rejects the promise
}).catch(alert); // Error: Whoops!
```

### **Common Promise utility methods: Promise.all(), Promise.race(), Promise.any(), Promise.allSettled()**

[Promise API](https://javascript.info/promise-api)

|Method|Description|
|---|---|
|Promise.all(iterable)|Resolves when all Promises in the iterable resolve successfully, or rejects immediately if any of them are rejected. Returns an array of resolved values.|
|Promise.allSettled(iterable)|Resolves when all Promises in the iterable have settled (resolved or rejected). Returns an array of objects indicating the status and result or reason for each Promise.|
|Promise.race(iterable)|Resolves or rejects as soon as the first Promise in the iterable settles (resolves or rejects). Returns the result or reason of the first settled Promise.|
|Promise.any(iterable) (ES2021)|Resolves as soon as any Promise in the iterable resolves successfully. Rejects with an AggregateError if all Promises are rejected, providing reasons for each rejection.|

## **Async/Await**

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