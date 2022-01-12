## Weird JS Behavior

### Code-

![Code](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/imiqqgcpwue8uyrd13gq.png)

### Output-

```
50
50
```

_In the code sample, we didn't even explicitly declare the variable but we are able to use without any error and it is available in global scope_

#### Explanation-

-   Older versions of JS allowed us to create variables **without explicitly declaring** them using the `var`, `let` or the `const` keyword.
-   There are a lot of downfalls to this, some of them being-

#### Downfalls-

-   JS creates these variables in **global scope** by default thus anyone can access them from outside the function and change them.
-   You can **mistype** a variable name and JS won't even give an **error**, instead it will create a new variable in the global scope because of this behavior.

## Solution: _Strict Mode_

### Introduction-

-   The "use strict" directive was new in ECMAScript version 5 indicating use of **strict mode** while running the code.
-   It is supported by all the modern browsers and since it is only a string, **even older versions** that don't understand it won't throw any error.
-   It prevents all the **bad code practices** in previous JS versions from turning into actual errors.
-   If declared at the beginning of a script, it **has global scope** whereas if it is used inside the function then it's scope is only for that block/**block scope**.

**Declaration example-**

```
"use strict";
x = 3.14;  // this will cause error
```

### Issues that "use strict" fixes-

1. If you mistakenly mistype a variable, if ran in strict mode, it will **throw an error** instead of creating a new global variable.
1. It prevents us from assigning values to **non-writable properties** by throwing an error. This wasn't the same in previous versions.
1. Keywords reserved for future JavaScript versions can not be used as variable names in strict mode.
1. Prevents us from **duplicating parameter names**.
1. Prevents us from writing to a read-only properties.
1. Prevents us from writing to a get-only property.

```
"use strict";
const obj = {get x() {return 0} };

obj.x = 3.14;            // This will cause an error
```

7.Prevents us from **deleting an undeletable property**.

```
"use strict";
delete Object.prototype; // This will cause an error
```

8.Prevents us from using **Octal** numerical literals and Octal escape characters. Example-

```
"use strict";
let x = 010; // gives error
let x = "\010"; // gives error
```

-   Check this [article](https://www.w3schools.com/js/js_strict.asp) for all the things that are not allowed in "use strict".

**Note- The "use strict" directive is only recognized at the beginning of a script or a function.**

<hr/>

## Hoisting-

-   Hoisting is JavaScript's default behavior of moving all the declarations at the **top of the scope** before code execution.
-   It could be **variable** declarations or **function** declarations or even class declarations.
    ![Hoisting](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gxhki733f22qn6ttrbzn.png)
    _Credits-[tutorialsteacher](https://www.tutorialsteacher.com/javascript/javascript-hoisting)_

### Example of variable hoisting-

#### Code-

```
x = 5 // doesn't give any error because of hoisting
console.log(x)

var x // this gets hoisted to the top of the scope
```

#### Output-

```
5
```

### Example of function hoisting-

#### Code-

```
console.log(hello()) // doesn't give any error because of hoisting

function hello(){ // this gets hoisted to the top of the scope
	return "hello world"
}
```

#### Output-

```
"hello world"
```

-   Variables declared with `let` and `const` are also hoisted but, unlike `var`, are not initialized with a default value such as `undefined`. A `ReferenceError` exception will be thrown if a variable declared with `let` or `const` is read before it is initialized. This is because they stay in a **Temporal Dead Zone** before they are explicitly declared. We will learn more about Temporal Dead Zone ahead.

#### Code-

```
console.log(x)

let x
x = 5
```

#### Output-

```
Uncaught ReferenceError: Cannot access 'x' before initialization
```

#### Code-

```
console.log(x)

const x = 5
```

#### Output-

```
Uncaught ReferenceError: Cannot access 'x' before initialization
```

-   All JavaScript **declarations are hoisted** but not for initialization. **Initialization** in variables using `var` keyword are **partially hoisted** but those using `let` or `const` keyword are not hoisted at all and give error.

-   **Partial hoisting** means that the JS engine before running the code line by line already knows that the **variable exists** and has some memory allocated (because of hoisting) but the value for it hasn't been set/ stored yet (it gets set when we actually **reach that line of code**) thus a default value of `undefined` is set and returned. This partial hoisting happens in case of variable **initialization using `var`** keyword.
    ![Partial Hoisting](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/28a00s8npi7rjy930p66.png)
    _Credits- [Sabih Rehman](https://medium.com/@sabih811)_

### Example 1

#### Code-

```
console.log(x)

var x = 5 // this is initialization, not a declaration
```

#### Output-

```
undefined
```

_This code does not work because initializations are not hoisted. It returns `undefined` because we have used `var` here that leads to partial hoisting as discussed above._

### Example 2

#### Code-

```
console.log(x)

let x = 5 // this is initialization, not a declaration
```

#### Output-

```
Uncaught ReferenceError: Cannot access 'x' before initialization"
```

_This is because variable initialization using `let` or `const` don't get hoisted._

## Temporal Dead Zone-

> The variables declared using `let` and `const` are not accessible before they are initialized with some value, and the phase between the starting of the execution of block in which the variable is declared using `let` or `const` **till that variable is being initialized** is called Temporal Dead Zone for the variable.

-   Accessing the variable before the initialization results in a [ReferenceError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError).

#### Code-

```
console.log(x)

let x
x = 5
```

#### Output-

```
Uncaught ReferenceError: Cannot access 'x' before initialization
```

> The term "temporal" is used because the **zone depends on the order of execution** (time) rather than the order in which the code is written (position). For example, the code below works because, even though the function that uses the `let` variable appears before the variable is declared, the function is called outside the TDZ.

#### Code-

```
{
    // TDZ starts at beginning of scope
    const func = () => console.log(letVar); // OK

    // Within the TDZ letVar access throws `ReferenceError`

    let letVar = 3; // End of TDZ (for letVar)
    func(); // Called outside TDZ!
}
```

#### Output-

```
3
```

### Temporal Dead Zone tricky example-

```
function test(){
   var foo = 33;
   if(foo) {
      let foo = (foo + 55); // ReferenceError
   }
}
test();
```

> The `if` block is evaluated because the outer `var foo` has a value. However due to lexical scoping this value is not available inside the block: the identifier `foo` inside the `if` block is the `let foo`. The expression `(foo + 55)` throws a `ReferenceError` because initialization of `let foo` has not completed — it is still in the **temporal dead zone**.

<hr/>
## Appendix-

1. [**Advanced JavaScript Series - Part 1**: Behind the scenes (JavaScript Engine, ATS, Hidden Classes, Garbage Collection)](https://dev.to/pranav016/advanced-javascript-series-part-1-behind-the-scenes-javascript-engine-ats-hidden-classes-garbage-collection-3ajj)
1. [**Advanced JavaScript Series - Part 2**: Execution Context and Call Stack](https://dev.to/pranav016/advanced-javascript-series-part-1-execution-context-and-call-stack-l1o)
1. [**Advanced JavaScript Series - Part 3**: Weird JS behavior, Strict Mode and Hoisting, Temporal Dead Zone](https://dev.to/pranav016/advanced-javascript-series-part-3-weird-js-behavior-strict-mode-and-hoisting-26a3)
 <hr/>

## References-

1. https://www.w3schools.com/js/js_strict.asp
2. https://www.w3schools.com/js/js_hoisting.asp
3. https://developer.mozilla.org/en-US/docs/Glossary/Hoisting
4. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const
5. https://www.geeksforgeeks.org/what-is-the-temporal-dead-zone-in-es6/#:~:text=The%20let%20and%20const%20variables,Dead%20Zone%20for%20the%20variable.
6. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let

_All codes implemented using JS Fiddle_
