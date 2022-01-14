## IIFE

> An IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined.

### Use cases-

#### Helps avoid polluting the global namespace-

-   Since our application may incorporate a large number of functions and global variables from various source files, it's critical to keep the number of global variables to a minimum.
-   We could utilise the IIFE pattern if we have some initiation code that we don't need to use again. Because we won't be reusing the code, IIFE is preferable than a function declaration or a function expression in this scenario.

### Example-

```
(function () {
  // some initiation code
  let firstVariable;
  let secondVariable;
})();
```

_`firstVariable` and `secondVariable` will be discarded after the function is executed._

#### The module pattern-

-   We would also use IIFE to create private and public variables and methods.
-   These patterns were more useful before the introduction of ES6, when we didn't have the `let` and the `const` keywords. Back then when we imported all the javascript files into one, then there were a lot of conflicts in variable names since all variables were global because of declaration using `var`. Thus developers used IIFE module patterns where the variables were made and only those required inside module were left in global scope and others were discarded because of property of Scope using IIFEs. This also overlaps with the first use case of IIFEs mentioned above. Consider this example to understand better-

##### Example-

> As you know that a function in JavaScript creates the local scope. So, you can define variables and function inside a function which cannot be access outside of that function. However, sometime you accidently pollute the global variables or functions by unknowingly giving same name to variables & functions as global variable & function names.

> For example, there are multiple .js files in your application written by multiple developers over a period of time. Single JavaScript file includes many functions and so these multiple .js files will result in large number of functions. There is a good chance of having same name of function exists in different .js files written by multiple developer and if these files included in a single web page then it will pollute the global scope by having two or more function or variables with the same name.

_Consider the following example of `MyScript1.js` and `MyScript2.js` with same variable & function name._

###### MyScript1.js

```
var userName = "Bill";

function display(name)
{
    alert("MyScript1.js: " + name);
}

display(userName);
```

###### MyScript2.js

```
var userName = "Steve";

function display(name)
{
    alert("MyScript2.js: " + name);
}

display(userName);
```

###### Importing both files-

```
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>JavaScript Demo</title>
    <script src="/MyScript1.js"></<script>
    <script src="/MyScript2.js"></<script>
</head>
<body>
    <h1> IIFE Demo</h1>
</body>
</html>
```

> If you run above example, you will find that every time it call display() function in MyScript2.js because MyScript2.js included after MyScript1.js in a web page. So JavaScript considers last definition of a function if two functions have the same name.

> IEFE solves this problem by having its own scope and restricting functions and variables to become global. The functions and variables declare inside IIFE will not pollute global scope even they have same name as global variables & functions. So let's see what is an IIFE is.

### Advantages of IIFE:

-   Helps avoid creating unnecessary global variables and functions.
-   Functions and variables defined in IIFE do not conflict with other functions & variables even if they have same name.
-   Organize JavaScript code.
-   Make JavaScript code maintainable.

_Check out this [documentation](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) and this [article](https://benalman.com/news/2010/11/immediately-invoked-function-expression/) to read more in-depth about IIFEs if required._

<hr/>

## `this` keyword-

> `this` represents the object that the function is a property of.

or simply

> `this` helps refer to the object it belongs to.

-   In a method, `this` refers to the owner object.

### Example-

#### Code-

```
const person = {
  firstName: "Pranav",
  lastName : "Mendiratta",
  fullName : function() {
    // here `this` keyword refers to our object `person`
    return this.firstName + " " + this.lastName;
  }
};
console.log(person.fullName())
```

#### Output-

```
"Pranav Mendiratta"
```

-   Alone, `this` refers to the global object (called the window object in the browser).

### Example-

#### Code-

```
console.log(this)
```

#### Output-

```
window
```

-   In a function, `this` refers to the global object.
-   In a function, in strict mode, `this` is undefined.
-   In an event, `this` refers to the element that received the event.

### Example-

#### Code-

```
<button onclick="this.style.display='none'">
  Click to Remove Me!
</button>
```

### Tricky example on `this` keyword 1

{% jsfiddle https://jsfiddle.net/rkjdpuez/2/ js %}

#### Output-

```
window
window
c
```

### Explanation-

-   Both `a` and `b` are functions of the global/ window object, thus as per the definition, the `window` object gets returned.

> `this` represents the object that the function is a property of.

-   The third `console.log` returns the `c` object because thats what has called the `hi()` function.

### Tricky example on `this` keyword 2

{% jsfiddle https://jsfiddle.net/gfvjLo2b/ js %}

#### Output-

```
obj
window
```

### Explanation-

-   On calling the `sing()` function, the `console.log(this)` on line 4 returns the `obj` object since `obj` is calling the function.
-   Whereas the `console.log(this)` on line 6 returns the `window` object because its function call is not attached to any object, and those not attached are always under the global/ window object.

### Tricky example on `this` keyword 3

{% jsfiddle https://jsfiddle.net/yut8g7La/ js %}

#### Output-

```
b
window
d
```

### Explanation-

-

### Tricky example on `this` keyword 4

```
const phone = function (model, brand){
  this.model = model,
  this.brand = brand
}

// regular anonymous  function used
phone.prototype.clickPicture = function(){
  console.log(`${this.brand} ${this.model} clicks picture!`)
}

// arrow function used here
phone.prototype.powerOn = () => {
  console.log(`${this.brand} ${this.model} boots up!`)
}

const iphone = new phone("Iphone 12", "Apple")
console.log(iphone.clickPicture())
console.log(iphone.powerOn())
```

#### Output-

```
"Apple Iphone 12 clicks picture!"
"undefined undefined boots up!"
```

### Explanation-

-   Arrow functions are lexically scoped where as regular anonymous functions are dynamically scoped.

### Conclusion-

-   Alot of the weird behavior of the `this` keyword is mainly because it is dynamically scoped and not lexically scoped like everything else in JavaScript meaning that it is not important where it is written but how it is called.

### Solution to weird behavior-

-   One way to solve these issues is the use of arrow functions that were introduced in ES6.
-   If we use an arrow function in the previous example then our function gives us the desired output.
-   Another way is to bind the `this` keyword to the object. We will learn more about `bind` keyword ahead.
<hr/>

## call()

> With the `call()` method, you can write a method that can be used on different objects.

### Example-

#### Code-

```
const wizard = {
  name: 'Pranav',
  health: 100,
  heal: function(num1, num2) {
    this.health += num1 + num2;
  }
}

const archer = {
  name: 'Robin',
  health: 50
}

wizard.heal.call(archer, 50, 60)
console.log(archer)
```

#### Output-

```
{
  health: 160,
  name: "Robin"
}
```

## apply()

> With the apply() method, you can write a method that can be used on different objects.

-   It is very similar to the `call` keyword, only difference is that the arguments are passed as an array when we are using `apply`.

### Example-

#### Code-

```
const wizard = {
  name: 'Pranav',
  health: 100,
  heal: function(num1, num2) {
    this.health += num1 + num2;
  }
}

const archer = {
  name: 'Robin',
  health: 50
}

wizard.heal.apply(archer, [20, 30])
console.log(archer)
```

#### Output-

```
{
  health: 100,
  name: "Robin"
}
```

## bind()

> The bind() method creates a new function that, when called, has its this keyword set to the provided value.

-   It let’s us explicitly define the value of this when calling a function.

-   It returns a new function that we can call.

### Example-

#### Code-

```
const wizard = {
  name: 'Pranav',
  health: 100,
  heal: function(num1, num2) {
    this.health += num1 + num2;
  }
}

const archer = {
  name: 'Robin',
  health: 50
}

const healArcher = wizard.heal.bind(archer, 50, 60);
healArcher()
console.log(archer)
```

_The js engine is creating a new instance of the heal function and binding its `this` object to archer._

#### Output-

```
{
  health: 160,
  name: "Robin"
}
```

## Currying-

> Currying is a technique of evaluating function with multiple arguments, into sequence of functions with single argument.

### Example 1-

#### Code-

```
function volume(length) {
      return function(width) {
         return function(height) {
            return height * width * length;
         }
      }
   }
console.log(volume(11)(2)(3))
```

#### Output-

```
66
```

### Example 2-

#### Code-

```
function sum(a, b) {
    return a+b;
}

var sumWithThree = sum.bind(this, 3);
console.log(sumWithThree(4));
```

#### Output-

```
7
```

<hr/>
## Appendix-

1. [**Advanced JavaScript Series - Part 1**: Behind the scenes (JavaScript Engine, ATS, Hidden Classes, Garbage Collection)](https://dev.to/pranav016/advanced-javascript-series-part-1-behind-the-scenes-javascript-engine-ats-hidden-classes-garbage-collection-3ajj)
1. [**Advanced JavaScript Series - Part 2**: Execution Context and Call Stack](https://dev.to/pranav016/advanced-javascript-series-part-1-execution-context-and-call-stack-l1o)
1. [**Advanced JavaScript Series - Part 3**: Weird JS behavior, Strict Mode and Hoisting, Temporal Dead Zone](https://dev.to/pranav016/advanced-javascript-series-part-3-weird-js-behavior-strict-mode-and-hoisting-26a3)
 <hr/>

## References-

1. https://developer.mozilla.org/en-US/docs/Glossary/IIFE
1. https://www.tutorialsteacher.com/javascript/immediately-invoked-function-expression-iife
1. https://www.w3schools.com/js/js_this.asp
1. https://www.w3schools.com/js/js_function_call.asp
1. https://www.w3schools.com/js/js_function_apply.asp
1. https://medium.com/@omergoldberg/javascript-call-apply-and-bind-e5c27301f7bb
1. https://www.tutorialspoint.com/what-is-currying-in-javascript
