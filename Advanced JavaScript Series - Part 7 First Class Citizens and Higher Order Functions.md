## First Class Citizens

> First-class citizenship simply means **being able to do what everyone else can do.** In JavaScript, functions are objects (hence the designation of first-class object).

-   JavaScript has all those abilities or features that are required to be a language having First Class Functions, hence functions are treated as First Class Citizens.

-   Let’s look at all the abilities of functions being a First Class Citizen.

### 1. Ability to treat functions as values-

#### Code-

```
var hello = function(){
  return "hello world"
}

console.log(hello())
```

#### Output-

```
"hello world"
```

### 2. Ability to Pass functions as arguments-

#### Code-

```
function hello(fn){
  fn()
}

hello(function() { console.log("hello world") })
```

#### Output-

```
"hello world"
```

### 3. Ability return a function from another function-

#### Code-

```
function hello(){
  return function() {
    return "hello world"
  }
}

var hi=hello()
console.log(hi())
```

#### Output-

```
"hello world"
```

-   Because this behavior of JS functions as first class citizens, we are also able to do functional programming that we will learn more about in further parts of our series.

## Higher Order Functions-

> A higher order function is a function that takes a function as an argument, or returns a function.

### Simplified Example-

#### Code-

```
const multiplyBy = (num1) => {
  return function (num2) {
    return num1 * num2;
  }
}

const multiplyByTwo = multiplyBy(2);
multiplyByTwo(4)
```

#### Output-

```
8
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
 <hr/>

## References-

1. https://www.developintelligence.com/blog/2016/10/javascript-functions-as-first-class-objects/
1. https://www.geeksforgeeks.org/what-is-first-class-citizen-in-javascript/
1. https://medium.com/javascript-scene/higher-order-functions-composing-software-5365cf2cbe99
