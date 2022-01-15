## Introduction-

-   There are two types of datatypes in JavaScript namely the primitive and non-primitive data-types.
-   Primitive data types means that are immutable, cannot be further broken down since they are the smallest unit any data can be in. Non-primitive are opposite to this and can consist of different primitive types.

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

_You can see here how a function is behaving like an object._

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
> This is because behind the scenes, JS adds a wrapper to it and the code becomes `console.log(Boolean(true).toString())` and as we know everything acts like an object hence we are able to call the `toString()` function from `Boolean`.

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

## References-

1. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures
