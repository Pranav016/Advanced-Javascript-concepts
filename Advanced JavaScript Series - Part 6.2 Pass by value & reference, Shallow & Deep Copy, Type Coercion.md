## Pass by Value-

> In JavaScript **pass by value**, the function is called by directly passing the **value of the variable** as the argument. Therefore, even changing the argument inside the function doesn’t affect the variable passed from outside the function.

-   It is important to note that in JavaScript, **all function arguments are always passed by value**. That is, JavaScript **copies the values** of the passing variables into arguments inside of the function.

![DataTypes](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/y1zr1i8nuk6y3sjz1dlo.png)
_Credits- [Reina Mitchell](https://levelup.gitconnected.com/pass-by-value-vs-pass-by-reference-in-javascript-82fa8736c9f7)_

### Example-

#### Code-

```
let a=5
let b=a

b++;
console.log(b)
console.log(a)
```

#### Output-

```
6
5
```

## Pass by Reference-

> In **Pass by Reference**, a function is called by **directly passing the reference/address** of the variable as the argument. Changing the argument inside the function affects the variable passed from outside the function.

<br/>
* In JavaScript, **objects and arrays** are always passed by reference.

### Example-

#### Code-

```
let obj1={
  a: 'a',
  b: 'b',
  c: 'c'
}

// shallow copying the object using the spread operator
let obj2={...obj1}
obj2.b='d'

console.log(obj2)
console.log(obj1)
```

or

```
let obj1={
  a: 'a',
  b: 'b',
  c: 'c'
}

// another way of copying the object
let obj2=Object.assign({}, obj1)
obj2.b='d'

console.log(obj2)
console.log(obj1)
```

#### Output-

```
{
  a: "a",
  b: "d",
  c: "c"
}
{
  a: "a",
  b: "b",
  c: "c"
}
```

-   But this is only a **shallow copy** of the original object.

> A **deep copy** means that all of the values of the new variable are copied and disconnected from the original variable. A **shallow copy** means that certain (sub-)values are still connected to the original variable.

-   Lets understand this with the help of an example.

### Example-

```
let obj1 = {
  a: 'a',
  b: 'b',
  c: {
    d: 'd'
  }
};

let obj2={...obj1}
obj2.c.d='f'

console.log(obj2)
console.log(obj1)
```

#### Output-

```
{
  a: "a",
  b: "b",
  c: {
    d: "f"
  }
}
{
  a: "a",
  b: "b",
  c: {
    d: "f"
  }
}
```

_As you can see that the new object is still connected to the original object it got the value from._

-   The problem with **shallow copy** is that, if the user makes changes to the complex object (update street property of address object) of the source object `userName`, it is also reflected in the Destination Object, since it points to the same memory address and vice-versa.

-   Thus we turn towards **Deep Copying**. Deep copying means that value of the new variable is disconnected from the original variable while a shallow copy means that some values are still connected to the original variable.

-   Lets understand deep copying with the help of an example.

### Example-

#### Code-

```
let obj1 = {
  a: 'a',
  b: 'b',
  c: {
    d: 'd'
  }
};

// converts obj1 to string and then parses it into a new object
let obj2 = JSON.parse(JSON.stringify(obj1))
obj2.c.d = 'f'

console.log(obj2)
console.log(obj1)
```

#### Output-

```
{
  a: "a",
  b: "b",
  c: {
    d: "f"
  }
}
{
  a: "a",
  b: "b",
  c: {
    d: "d"
  }
}
```

-   Here we can see that changes made in `obj2` are not reflected in `obj1` thus we can say that its a deep copy and the **two objects are disconnected**.

### How to compare two objects having different memory location but same value-

-   To answer this question, I have found this Stack Overflow thread that answer this question flawlessly and I couldn't explain it any better than thus adding the link to this thread: [Stack Overflow thread](https://stackoverflow.com/questions/1068834/object-comparison-in-javascript)

-   If the link due to any reason doesn't open, here is the fastest and limited way of comparing values of objects at different memory locations-

```
JSON.stringify(obj1) === JSON.stringify(obj2)
```

![Example](https://miro.medium.com/max/1000/1*Drz5Lwh2WtLcZdrxXg7JTQ.gif)
_Credits- Mathwarehouse_

<hr/>

### Tricky question to test knowledge-

```
const number = 100
const string = "Jay"
let obj1 = {
  value: "a"
}
let obj2 = {
  value: "b"
}
let obj3 = obj2;

function change(number, string, obj1, obj2) {
    number = number * 10;
    string = "Pete";
    obj1 = obj2;
    obj2.value = "c";
}

change(number, string, obj1, obj2);

// guess which variables will get updated
console.log(number);
console.log(string);
console.log(obj1.value);
```

### Output-

```
100
Jay
a
```

## Type Coercion-

> Type coercion is the automatic or implicit conversion of values from one data type to another (such as strings to numbers).

![Table](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3snzvcjric0z27bk5bwx.png)
_Credits- [Bill](https://stackoverflow.com/questions/359494/which-equals-operator-vs-should-be-used-in-javascript-comparisons)_

### Example-

#### Code-

```
const value1 = '5';
const value2 = 9;
let sum = value1 + value2;

console.log(sum);
```

#### Output-

```
"59"
```

-   In the above example, JavaScript has coerced the **9 from a number into a string** and then **concatenated** the two values together, resulting in a string of 59. JavaScript had a choice between a string or a number and decided to use a string.

-   The compiler could have coerced the 5 into a number and returned a sum of 14, but it did not. To return this result, you'd have to **explicitly convert** the 5 to a number using the `Number()` method:

```
sum = Number(value1) + value2;
```

As an example of type coercion in practice, look at the [JavaScript Comparison Table](https://dorey.github.io/JavaScript-Equality-Table/), which shows how the loose equality `==` operator behaves for different types.

### Implicit vs. explicit coercion

-   Type coercion can be explicit and implicit.

-   When a developer expresses the intention to convert between types by writing the appropriate code, like Number(value), it’s called **explicit type coercion** (or type casting).

-   Since JavaScript is a [weakly-typed language](https://en.wikipedia.org/wiki/Strong_and_weak_typing), values can also be converted between different types automatically, and it is called **implicit type coercion**.

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
 <hr/>

## References-

1. https://flexiple.com/javascript-pass-by-reference-or-value/
2. https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion
3. https://www.freecodecamp.org/news/js-type-coercion-explained-27ba3d9a2839/
