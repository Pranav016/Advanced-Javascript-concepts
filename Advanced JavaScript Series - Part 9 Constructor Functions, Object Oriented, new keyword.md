## Constructor Functions-

-   In JavaScript, a **constructor function** is used to create objects.
-   It is considered good practice to name constructor functions with an **upper-case first letter**.

### Example-

#### Code-

```
const Phone = function (model, brand){
  this.model = model,
  this.brand = brand
}

phone.prototype.clickPicture = function(){
  console.log(`${this.brand} ${this.model} clicks picture!`)
}

const iphone = new Phone("Iphone 12", "Apple")
console.log(iphone.clickPicture())
```

-   In the above example, function `Phone()` is an object constructor function.

-   To create an object from a constructor function, we use the `new` keyword.

#### Output-

```
"Apple Iphone 12 clicks picture!"
```

### Built-in constructors-

#### Example-

```
let a = new Object();    // A new Object object
let b = new String();    // A new String object
let c = new Number();    // A new Number object
let d = new Boolean();   // A new Boolean object
```

-   All these are constructor functions provided to us by javascript.

##### Code-

```
typeof Object
```

##### Output-

```
'function'
```

## Classes-

-   Another way of creating templates for JavaScript Objects are **Classes**.
-   They are very similar to constructor functions. Classes have their own constructors that help initialize variables/values.

### Constructor method-

The constructor method is a special method:

-   It has to have the exact name "constructor"
-   It is executed automatically when a new object is created
-   It is used to initialize object properties

<br> <br>

-   If you do not define a constructor method, JavaScript will add an empty constructor method.
-   Just like constructor functions, we can use the `new` keyword to create new objects from this class.

### Example-

#### Code-

```
class Phone{
  constructor(model, brand){
    this.model = model
    this.brand = brand
  }
  clickPicture() {
    console.log(`${this.brand} ${this.model} clicks picture!`)
  }
}

const iphone = new Phone("Iphone 12", "Apple")
console.log(iphone.brand)
console.log(iphone.clickPicture())
```

-   Here `iphone` is an instance of the class `Phone`.
-   There is a reason why we do not call the `clickPicture` function from inside the constructor because, the constructor is called every time we instantiate a new object and that would initialize the function every time instead of sharing it among objects thus taking up more space in memory.

#### Output-

```
"Apple"
"Apple Iphone 12 clicks picture!"
```

-   Classes in JavaScript is just syntactical sugar but under the hood it still uses **prototypal inheritance**.

### Inheritance in Classes-

> Inheritance enables you to define a class that takes all the functionality from a parent class and allows you to add more. Using class inheritance, a class can inherit all the methods and properties of another class.

-   The `super()` method refers to the parent class.

![Inheritance ](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/56zl2zgjto5031ej6yki.png) _Credits- [Rupesh Mishra](https://medium.com/@happymishra66)_

#### Example-

##### Code-

```
class Phone{
  constructor(model, brand){
    this.model = model
    this.brand = brand
  }
  clickPicture() {
    console.log(`${this.brand} ${this.model} clicks picture!`)
  }
}

class Iphone extends Phone {
  constructor(model, brand, software){
    super(model, brand)
    this.software = software
  }
}

const tenPro = new Iphone("10 pro", "Apple", "IOS")
console.log(tenPro)
```

##### Output-

```
{
  brand: "Apple",
  model: "10 pro",
  software: "IOS"
}
```

## `new` keyword in JS

> The new operator lets developers create an instance of a user-defined object type or of one of the built-in object types that has a constructor function.

### Example-

#### Code-

```
function Car(make, model, year, owner) {
  this.make = make;
  this.model = model;
  this.year = year;
  this.owner = owner;
}
```

#### Output-

```
var car1 = new Car('Eagle', 'Talon TSi', 1993, rand);
var car2 = new Car('Nissan', '300ZX', 1992, ken);
```

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
1. [**Advanced JavaScript Series - Part 8**: The 2 Pillars~ Closures & Prototypal Inheritance](https://dev.to/pranav016/advanced-javascript-series-part-8-the-2-pillars-closures-prototypal-inheritance-4m5n)
 <hr/>

### References-

1. https://www.programiz.com/javascript/constructor-function
1. https://www.w3schools.com/js/js_object_constructors.asp
1. https://www.w3schools.com/js/js_class_intro.asp
1. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new
1. https://www.programiz.com/javascript/inheritance
1. https://www.w3schools.com/js/js_class_inheritance.asp
