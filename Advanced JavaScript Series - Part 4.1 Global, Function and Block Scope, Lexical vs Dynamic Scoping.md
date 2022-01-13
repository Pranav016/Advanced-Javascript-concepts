## What is Scope?
> In simple terms, **Scope** can be defined as the space in which variables and statements **are accessible**.

or
> Scope determines **the accessibility** of variables, objects, and functions from different parts of the code.

* Let's understand this definition with an example- 

### Example-
```
var x = 2

function myFunc(){
  console.log(x)
}
```
*myFunc function is able to access the variable `x` thus we can say that `x` is in scope of myFunc.*

* Before ES6 (2015), there were only 2 types of scope (Global and Function) but in ES6, a new scope was introduced, namely the **Block Scope**.

## 3 types of Scopes:

![Scope](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2xounixbcpualerc4k8z.png)*Credits-[Nemo](https://dev.to/nemo011)*


### 1. Global Scope-
* Variables declared globally/ in the global execution context have a global scope.
* They can be **accessed from anywhere** in the program.
* No matter whether they are declared using `var`, `let` or `const`, variables declared in global scope behave similarly.

#### Example-
```
var x = 2

function myFunc(){
  console.log(x)
}
```
*Here the variable `x` is declared in global scope thus it is available for use across the entire program.*

* As explained in [Part 3](https://dev.to/pranav016/advanced-javascript-series-part-3-weird-js-behavior-strict-mode-and-hoisting-26a3) of this Advanced JavaScript series, if a variable is declared without `var`, `let` or `const` keyword, it always gets declared in the **global scope**.

#### Example-
```
function myFunc(){
  x = 1
}
console.log(x)
```
*Here the code gives output `1` since the variable `x` gets declared in Global scope.*

### 2. Function/Local Scope-
* Variables declared within a JavaScript function, become **LOCAL** to the function.
* These variables can only be **accessible from within** the function.
* These variables are **removed from the memory** when the execution of the function is completed thus the variable names can be reused in some other functions.
* All `var`, `let` and `const` work similarly in Function scope. 

#### Example-
```
function myFunc(){
  let x = 1
  console.log(x)
}
```
*Here the variable `x` is declared in the function/local scope thus accessible only from inside the function.*

### 3. Block Scope-
* The two new keywords for variable declaration, that is `let` and `const` that were introduced in ES6 are Block Scoped.
* Any variable that is declared within a pair of braces { } or a block and cannot be accessed from outside it are said to be **Block Scoped**.

#### Example-
```
var x = 1
if(x){
  var y = 2
  let z = 3
  console.log("hello world")
}
console.log(y)
console.log(z)
```

#### Output-
```
2
Uncaught ReferenceError: z is not defined
```
*Here, the variable `y` cannot be accessed from outside the `if block` because variables declared using `let` are Block Scoped whereas variables declared using `var` are not.*

## Lexical vs Dynamic Scoping-

* In **Lexical(Static) Scoping**, the structure of the program source code determines what variables you are referring to.
* In **Dynamic Scoping**, the runtime state of the program stack determines what variable you are referring to.

> **Lexical scoping** refers to the variables in the location of a function's definition, whereas **dynamic scoping** refers to the variables in the location of a function's invocation.

* Let's understand with the help of an example.

### Example-

#### Code-
```
function a() { 
    console.log(i);
}

function b() {
    var i = 1;
    a();
}

var i = 0;

b();
```
#### Explanation-

> We have two function, `a` and `b`. `a` logs out the value of `i` which is set globally to `0`. `b` sets its value to `1`, and calls `a`. If we call `b`, it will log out `0`. This is because — while `a` doesn't have a variable called `i` — `a` has access to the enclosing scope where the function is defined. And in the global scope, we have an `i` which is set to `0`. This is called lexical scoping.

> In dynamic scoping, the value of `i` will be `1`. This is because instead of looking at where the function is defined, it looks at where it is called from. It sees from the call stack that it has been called from `b`, which sets the value of `i` to be `1`.

* As you can see, lexical scope looks at where a **function is declared**, where dynamic scope refers to where a **function is called** from.

![Scoping](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/r4ix3u3wqemix3cfi2sj.png)*Credits-[Thang Tran Duc](https://www.slideshare.net/thangtd90/javascript-under-the-hood-1)*
 

<hr/>
## Appendix-

1. [**Advanced JavaScript Series - Part 1**: Behind the scenes (JavaScript Engine, ATS, Hidden Classes, Garbage Collection)](https://dev.to/pranav016/advanced-javascript-series-part-1-behind-the-scenes-javascript-engine-ats-hidden-classes-garbage-collection-3ajj)
1. [**Advanced JavaScript Series - Part 2**: Execution Context and Call Stack](https://dev.to/pranav016/advanced-javascript-series-part-1-execution-context-and-call-stack-l1o)
1. [**Advanced JavaScript Series - Part 3**: Weird JS behavior, Strict Mode and Hoisting, Temporal Dead Zone](https://dev.to/pranav016/advanced-javascript-series-part-3-weird-js-behavior-strict-mode-and-hoisting-26a3)
<hr/>


## References-

1. https://www.w3schools.com/js/js_scope.asp
1. https://stackoverflow.com/questions/22394089/static-lexical-scoping-vs-dynamic-scoping-pseudocode
1. https://www.webtips.dev/webtips/javascript-interview/lexical-vs-dynamic-scoping