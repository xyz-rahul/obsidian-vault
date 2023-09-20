# Objects

“Objects can be created with object literals, with the new keyword, and with the Object.create()”

# Prototypes

“Almost every JavaScript object has
a second JavaScript object associated with it. This second object is
known as a prototype, and the first object inherits properties from
the prototype.”

“So the object created by new Object() inherits from Object.prototype, just as the object created by {} does. Similarly, the object created by new Array() uses Array.prototype as its prototype, and the object created by new Date() uses Date.prototype as its prototype. This can be confusing when first learning JavaScript. Remember: almost all objects have a prototype, but only a relatively small number of objects”have a prototype property. It is these objects with prototype properties that define the prototypes for all the other objects.”

“Object.prototype is one of the rare objects that has no prototype:
it does not inherit any properties. Other prototype objects are normal
objects that do have a prototype. Most built-in constructors (and most
user-defined constructors) have a prototype that inherits from
Object.prototype”

## Object.create()

Object.create() creates a new object, using its first argument as
the prototype of that object:”

```javascript

“let o1 = Object.create({x: 1, y: 2});     // o1 inherits properties x and y.
o1.x + o1.y   ”

```

	“You can pass null to create a new object that does not have a
	prototype, but if you do this, the newly created object will not
	inherit anything, not even basic methods like toString() (which
	means it won’t work with the + operator either)”

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

## 