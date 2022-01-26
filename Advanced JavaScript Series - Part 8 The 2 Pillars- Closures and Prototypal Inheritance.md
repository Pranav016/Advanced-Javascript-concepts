## Closures-

> A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/784dqhmvns1kc5yl25ui.png) _Credits- [Edward Huang](https://edwardgunawan880.medium.com/)_

-   Lets understand concept of closures with the help of examples.
-   Closures have two major advantages.

### 1. Memory efficient

#### Example 1-

-   We want to build a counter function that keeps a track of counts and the count gets increased on calling the function. For that we'll need a `count` variable initialized to zero.
-   But we don't want it to be accessed by anyone else and alter it thus we **don't want the `count` variable to be in a global scope** for this very reason.
-   We can't declare it inside the function either because whenever the function will be called, it will create a new execution context that creates **a new local scope** for the function(we have learned this in previous parts of our series). Thus the `count` variable gets reinitialized to zero **every time we call the function**, hence we **can't declare it in local/functional scope** either.
-   We can also try to use nested functions just like this-

```
function add() {
  let counter = 0;
  function plus() {counter += 1;}
  plus();
  return counter;
}
```

_But here we can't call the `plus()` function from outside hence this is of no use._

-   Here comes the concept of closures and self invoked functions(learned in earlier parts of the series).

> A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).

```
const add = (function () {
  let counter = 0;
  return function () {counter += 1; return counter}
})();

add();
add();
add();
```

-   Here as you can see the **function that we return** from the self invoked function has a **reference of a variable** that is outside its local environment just like we said in closures- `with references to its surrounding state`.
-   These references from external environment are stored in the memory even if **we lose the function outside** because the particular reference is being used in the **function we call**.
-   That's why closures are very a powerful concept.

#### Example 2-

##### Code-

```
const getHeavy = heavy();
console.log(getHeavy(699))
console.log(getHeavy(700))
console.log(getHeavy(701))

// we don't want to pollute global namespace
function heavy() {
  const bigArray = new Array(7000).fill('hello')
  return function(item) {
    return bigArray[item]
  }
}
```

-   Here we are returning a function that can access the required index whenever called, **without polluting our global namespace**.
-   Here the **reference to the array** `bigArray` **stays in memory** even though the outer function is popped from the call stack and its context is removed because of the concept **of closures** and we are able to use the `getHeavy` function to access required indexes from it.

#### Output-

```
"hello"
"hello"
"hello"
```

### 2. Encapsulation

-   We can make variables that are not accessible in the global scope by anyone or any function.
-   We can also make variables that are **accessible via a function without it being in its local scope** such that it gets destroyed when its execution context is popped of the call stack.
-   We can make variables encapsulated and safe with the help of closures.

#### Example-

##### Code-

```
const getHeavy = heavy();
console.log(getHeavy(699))
console.log(getHeavy(700))
console.log(getHeavy(701))

// we don't want to pollute global namespace
function heavy() {
  const bigArray = new Array(7000).fill('hello')
  return function(item) {
    return bigArray[item]
  }
}
```

-   The `bigArray` cannot be accessed from anywhere in the function except for the function that we return to the `getHeavy` variable.
-   In this way the array is encapsulated, we can access it anytime, from anywhere without it being declared in the global namespace/scope and this is property is very useful in different scenarios.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/q3gn8neke3498qnci68f.png) _Credits- [Neelesh Vishwakarma](https://www.c-sharpcorner.com/members/neelesh-vishwakarma)_

## Prototypal Inheritance-

> Prototypal Inheritance is a method by which an object can inherit the properties and methods of another object.

-   All JavaScript objects inherit properties and methods from a prototype.

*   Date objects inherit from `Date.prototype`
*   Array objects inherit from `Array.prototype`
*   Person objects inherit from `Person.prototype`
*   The `Object.prototype` is on the top of the prototype inheritance chain:

*   Date objects, Array objects, and Person objects inherit from `Object.prototype`.
*   And if we check the prototype of the `Object` then we see `null` being returned by JavaScript since Object is root element in JS.

![Inheritance](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v69ewr3k3sv9sq5w2u8u.png)
_Credits- [Ryan Thelin](https://www.educative.io/blog/understanding-and-using-prototypal-inheritance-in-javascript)_

-   `__proto__` is another keyword that can help us determine the parent/prototype of any object(even array or function) in javascript.

Let's see this with help of an example-

### Example 1-

-   Let's make an object for a phone that would have all the basic properties that a phone should have.
-   Then we would make an Object for an iPhone, that would inherit the properties from the generic phone object to specify all the basic features and then add its own specific features to the iPhone object(itself).

-   We also have a `isPrototypeOf()` method that checks if an object exists in another object's prototype chain.

> The `hasOwnProperty()` method returns a boolean indicating whether the object has the specified property as its own property (as opposed to inheriting it).

#### Code-

```
const phone = {
  calling: true,
  camera: true,
  touchscreen: true,
}

const iphone = {
  software: "IOS",
  security: "Face Unlock",
}

iphone.__proto__ = phone
console.log(iphone.calling)
console.log(phone.isPrototypeOf(iphone))
console.log(phone.hasOwnProperty(camera))
```

-   In this example, when run `console.log(iphone.calling)`, the JS engine checks iphone's properties and looks for the key `calling`.
-   When we use **prototypal inheritance**, the properties don't get added to the child object itself. That is why, when we access a property that is not there in the child object, the JS engine continues its **searches up the prototype chain in parent object's** properties and returns if found.
-   If not found, `undefined` is logged on the console.
-   This above is the reason, false is returned, when we run `console.log(phone.hasOwnProperty(camera))` because the iphone object doesn't have the `camera` property natively, instead it is inherited from the prototytpe.

#### Output-

```
true
true
false
```

### Example 2-

-   `__proto__` always **returns the parent object of our current object** that it **inherits** its properties from.
-   If we take an array or a function and access `__proto__` property of either one, firstly we'll see their respective objects in the output.
-   But if we further access the `__proto__` property of their outputs then we get the constructor object "Object" that is the base unit of arrays, functions, objects etc in JavaScript.
-   We cannot go any further back than the Object property. Behind that we only receive `null`.

#### Code-

```
const phone = {
  calling: true,
  camera: true,
  touchscreen: true,
}

const iphone = {
  software: "IOS",
  security: "Face Unlock",
}

iphone.__proto__ = phone
console.log(iphone.__proto__) // we recieve phone object
console.log(iphone.__proto__.__proto__) // we get the base constructor object
console.log(iphone.__proto__.__proto__.__proto__) // we get null here since we cannot go further back than an Object which is base unit
```

#### Output-

![Output1](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5mc06oqma8fa0hck9gna.png)

-   `prototype` keyword in JavaScript is always present in the parent object that holds all the properties that would be inherited down to its child. It also holds the parent object's own `__proto__` property to access its parent.

### Example to help understand-

#### Code-

```
const phone = {
  calling: true,
  camera: true,
  touchscreen: true,
}

const iphone = {
  software: "IOS",
  security: "Face Unlock",
}

iphone.__proto__ = phone
console.log(iphone.prototype)
```

-   Traditionally, in order to get and set the `[[Prototype]]` of an object, we use `Object.getPrototypeOf` and `Object.setPrototypeOf`. Nowadays, in modern language, it is being set using `__proto__`.

-   One reason to use the built-in prototype object is if you'll be duplicating an object multiple times that will share common functionality. By attaching methods to the prototype, you can save on duplicating methods being created per each new instance.

-   `__proto__` is an object in every class instance that points to the prototype it was created from.

-   The only true difference between `prototype` and `__proto__` is that the **former is a property of a class constructor**, while the latter is a **property of a class instance**.

-   `__proto__` is the actual object that is used in the lookup chain to resolve methods, etc. `prototype` is the object that is used to build `__proto__`.

-   Updating the `__proto__` property is not a good practice, instead a good way to inherit properties is by using `Object.create()`.

### Another way of creating a prototype chain `Object.create()`

> ECMAScript 5 introduced a new method: `Object.create()`. Calling this method creates a new object. The prototype of this object is the first argument of the function.

### Example-

#### Code-

```
const phone = {
  calling: true,
  camera: true,
  touchscreen: true,
}

const iphone = Object.create(phone)

iphone.software= "IOS",
iphone.security= "Face Unlock"

console.log(iphone.calling)
```

#### Output-

```
true
```

Some useful articles-

-   https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
-   https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes

### Tricky example to test knowledge about prototype chain-

#### Code-

```
const multiply = function(a, b){
  return a*b
}

console.log(multiply.__proto__)
console.log(Function.prototype)
console.log(multiply.__proto__.__proto__)
console.log(Object.prototype)

console.log(typeof Object)
console.log(typeof Object.prototype)
```

#### Output-

```
Function constructor
Function constructor
Object constructor
Object constructor
'function'
'object'
```

-   `Object` is an inbuilt function in JavaScript. It also has a prototype of its own like all the other functions in JS.
-   `Object.prototype` returns an `'object'` as output since the base element/parent of a function is the **object constructor in JavaScript**. (as we learned before)

<hr/>
## Connect with me-
- [GitHub](https://github.com/Pranav016)
- [LinkedIn](https://www.linkedin.com/in/pranav-mendiratta/)

<hr/>
## Appendix-

1. [**Advanced JavaScript Series - Part 1**: Behind the scenes (JavaScript Engine, ATS, Hidden Classes, Garbage Collection)](https://dev.to/pranav016/advanced-javascript-series-part-1-behind-the-scenes-javascript-engine-ats-hidden-classes-garbage-collection-3ajj)
1. [**Advanced JavaScript Series - Part 2**: Execution Context and Call Stack](https://dev.to/pranav016/advanced-javascript-series-part-1-execution-context-and-call-stack-l1o)
1. [**Advanced JavaScript Series - Part 3**: Weird JS behavior, Strict Mode and Hoisting, Temporal Dead Zone](https://dev.to/pranav016/advanced-javascript-series-part-3-weird-js-behavior-strict-mode-and-hoisting-26a3)
1. [**Advanced JavaScript Series - Part 4.1**: Global, Function and Block Scope, Lexical vs Dynamic Scoping](https://dev.to/pranav016/advanced-javascript-series-part-41-global-function-and-block-scope-lexical-vs-dynamic-scoping-20pg)
1. [**Advanced JavaScript Series - Part 4.2**: Scope Chains and their working, Lexical and Variable Environments](https://dev.to/pranav016/advanced-javascript-series-part-42-scope-chains-and-their-working-lexical-and-variable-environments-19d5)
1. [**Advanced JavaScript Series - Part 5**: IIFE & 'this' keyword in JS(tricky Eg.), call(), apply(), bind(), Currying(Functional Prog)](https://dev.to/pranav016/advanced-javascript-series-part-5-iife-this-keyword-in-jstricky-eg-call-apply-bind-curryingfunctional-prog-98c)
1. [**Advanced JavaScript Series - Part 6.1**: Everything in JS is an Object? Weird JS behaviors revealed, Primitive Non-Primitive Types](https://dev.to/pranav016/advanced-javascript-series-part-61-everything-in-js-is-an-object-primitive-non-primitive-types-1d8c)
1. [**Advanced JavaScript Series - Part 6.2**: Pass by Value & Pass by Reference, Shallow & Deep Copy, Type Coercion](https://dev.to/pranav016/advanced-javascript-series-part-62-pass-by-value-pass-by-reference-shallow-deep-copy-type-coercion-49f3)
1. [**Advanced JavaScript Series - Part 7**: First Class Citizens & Higher Order Functions](https://dev.to/pranav016/advanced-javascript-series-part-7-first-class-citizens-higher-order-functions-3cda)
 <hr/>

## References-

1. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
1. https://www.geeksforgeeks.org/prototypal-inheritance-using-__proto__-in-javascript/
1. https://javascript.plainenglish.io/proto-vs-prototype-in-js-140b9b9c8cd5
1. https://stackoverflow.com/questions/4736910/javascript-when-to-use-prototypes
1. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isPrototypeOf
1. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty
