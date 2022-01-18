## What is a Scope Chain?

> The Scope Chain is the hierarchy of scopes that will be searched in order to find a function or variable.

![Scope Chain](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kz8mt8i5eo0plhotv8j1.png)
_Credits- [Anuradha Aggarwal](https://hashnode.com/@anuradha)_

-   When a variable is used in JavaScript, the **JavaScript engine** will try to find the variable’s value in the current scope. If it could not find the variable, it will look into the outer scope and will continue to do so until it finds the variable or reaches **global scope**.
-   If it’s still could not find the variable, it will either **implicitly declare the variable** in the global scope (if not in strict mode) or return an **error**.
-   The Scope Chain is used to **resolve variables**. When asked to resolve a variable, JavaScript always starts at the **innermost level** of the code nest and keeps jumping back to the parent scope until it finds the variable or any other resource it is looking for.
-   The scope chain can simply be defined as an **object** that contains a bunch of other objects. Each object has the **variable-to-value mapping** for its particular execution context.

### Example-

#### Code-

```
let c = 10
function a() {
  let b = 25;
  console.log('Inside function a()');
}
a();
```

#### Sample Scope chain object for the function `a`-

```
functionLexicalEnvironment = {
  environmentRecord: {
      b    : 25,
  }
  outer: {
    c  : 10,
  }
}
```

## Lexical Environment-

> A lexical environment is a structure that holds **identifier-variable mapping**.
> (here identifier refers to the name of variables/functions, and the variable is the reference to actual object [including function object and array object] or primitive value).

-   Simply put, a lexical environment is a place where **variables and references to the objects** are stored.

-   A lexical environment conceptually looks like this:

```
lexicalEnvironment = {
  environmentRecord: {
    <identifier> : <value>,
    <identifier> : <value>
  }
  outer: < Reference to the parent lexical environment>
}
```

-   Let's understand this with the help of an example-

```
let language = 'JS';
function a() {
  let b = 25;
  console.log('Inside function a()');
}
a();
console.log('Inside global execution context');
```

-   The JavaScript engine creates a new **lexical environment** to store the variables and functions defined in the global scope when it establishes a **global execution context** to execute global code. As a result, the lexical environment for the global scope will be as follows:

```
globalLexicalEnvironment = {
  environmentRecord: {
      language    : 'JS',
      a : < reference to function object >
  }
  outer: null
}
```

-   Because there is no outer **lexical environment** for the global scope, the outer lexical environment is set to `null`.

-   When the engine establishes an **execution context** for the `a()` function, it also creates a lexical environment in which variables defined in the function can be stored while the function is being executed. As a result, the function's **lexical environment** will look like this:

```
functionLexicalEnvironment = {
  environmentRecord: {
      b    : 25,
  }
  outer: <globalLexicalEnvironment>
}
```

-   Because the function is surrounded by the **global scope** in the source code, the function's outer lexical environment is set to the global lexical environment.

-   When a function finishes executing, its execution context is removed from the stack, but its lexical environment **may or may not be erased from memory**, depending on whether it is referenced by any other lexical environments in their **outer lexical environment property**.

# Variable Environment-

> The variable environment is a representation of the **lexical environment’s local memory**. In the environment record, the lexical environment stores variables as well as other information such as the infamous this.

-   We've previously used one variable environment, the **global environment's memory**, which holds variables that are universally available throughout the script. While the lexical environment refers to this global environment, the variable environment only refers **to variables created within the scope** of the provided function within the lexical environment.

-   The variable environment **maps the local scope** of a given environment. In other words, the variable environment stores those variables defined within the given working code block `{}`.

![Img](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/olf5ymfxixmr88y5i2jf.png)

_Credits- [Benjamin Gruenbaum](https://stackoverflow.com/users/1348195/benjamin-gruenbaum)_

<hr/>

## Appendix-

1. [**Advanced JavaScript Series - Part 1**: Behind the scenes (JavaScript Engine, ATS, Hidden Classes, Garbage Collection)](https://dev.to/pranav016/advanced-javascript-series-part-1-behind-the-scenes-javascript-engine-ats-hidden-classes-garbage-collection-3ajj)
1. [**Advanced JavaScript Series - Part 2**: Execution Context and Call Stack](https://dev.to/pranav016/advanced-javascript-series-part-1-execution-context-and-call-stack-l1o)
1. [**Advanced JavaScript Series - Part 3**: Weird JS behavior, Strict Mode and Hoisting, Temporal Dead Zone](https://dev.to/pranav016/advanced-javascript-series-part-3-weird-js-behavior-strict-mode-and-hoisting-26a3)
1. [**Advanced JavaScript Series - Part 4.1**: Global, Function and Block Scope, Lexical vs Dynamic Scoping](https://dev.to/pranav016/advanced-javascript-series-part-41-global-function-and-block-scope-lexical-vs-dynamic-scoping-20pg)
 <hr/>

## References-

1. https://anuradha.hashnode.dev/scope-chain-and-lexical-environment-in-javascript
1. https://blog.bitsrc.io/understanding-scope-and-scope-chain-in-javascript-f6637978cf53
1. https://medium.com/@bdov_/javascript-typescript-execution-vs-lexical-vs-variable-environment-37ff3f264831
1. https://stackoverflow.com/questions/20721626/value-of-variable-and-lexical-environment-after-creating-execution-context
