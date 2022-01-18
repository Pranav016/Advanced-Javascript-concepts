## Introduction-

-   There are two types of datatypes in JavaScript namely the primitive and non-primitive data-types.
-   Primitive data types means that are immutable, cannot be further broken down since they are the smallest unit any data can be in. Non-primitive are opposite to this and can consist of different primitive types.

![DataTypes](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tiq8n9z3hsbimcdy17kb.png)
_Credits- [Deepali](https://www.naukri.com/learning/articles/javascript-data-types-with-examples/)_

### Primitive type includes-

1. Boolean
1. Null
1. Undefined
1. Number
1. BigInt
1. String
1. Symbol

### Non-Primitive Types includes-

1. Objects

-   You must be wondering what about arrays and functions? Well, in JavaScript both arrays and functions are a form of object even though when we do `typeof` on a function it returns `function` but it is an object. Check these examples to understand better.

### Examples-

#### Code 1-

```
function a(){
  console.log("hello world")
}

a.hi = "hi"
console.log(a.hi)
```

#### Output 1-

```
"hi"
```

_You can see here how a function is behaving like an object. How we were able to add a new property to the function._

#### Code 2-

```
typeof []
```

#### Output 2-

```
'object'
```

_You can see here how an array is returning `object` as its type._

-   But in real, everything in JavaScript behaves as an object. Check out this [documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects) and see how `Number`, `String` and many more are listed as built-in objects in JavaScript.
-   Let's see this with the help of an example.

### Example-

#### Code-

```
console.log(true.toString())
```

#### Output-

```
'true'
```

> You can see how a boolean value is acting like an object.

This is because behind the scenes, JS adds a wrapper to it and the code becomes `console.log(Boolean(true).toString())` and as we know everything acts like an object hence we are able to call the `toString()` function from `Boolean`.

## If an array is an object, how would we differentiate incase we need to-

-   There are many different functions available in JS that help us differentiate the types from one anther.
-   For example, in JS a new function was introduced that helps differentiate array from objects.

### Example-

#### Code-

```
var x=[1,2,3]
Array.isArray(x)
```

#### Output-

```
true
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
 <hr/>

## References-

1. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures
