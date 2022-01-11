## Execution Context-
* **Execution context** is the environment that enables JavaScript code to execute. It decides which piece of code currently gets access to all the functions, variables and objects used in the code for its execution.
* In this the code gets evaluated line by line, variables & objects etc get stored in the *[Memory heap](https://levelup.gitconnected.com/understanding-call-stack-and-heap-memory-in-js-e34bf8d3c3a4)* that are then used during the execution of that piece of code thus forming an environment that enables execution of the JS code.

## Call Stack/ Execution Stack-
* **Call Stack** is a data-structure that maintains the list of the functions being called and executed/ the execution context currently being executed by the JavaScript engine.
* It follows a **LIFO** (Last-In, First-Out) principle, meaning that the last function called gets to the top of the call stack and once execution is finished, it pops from the stack.
![Execution Stack](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bq1t5b5um9t4ad7ienh5.png)
*Credits- [Babs Craig](https://babscraig.com/)*
<hr/>
**Note-**
- Natively, JavaScript is a **single-threaded**, synchronous programming language. *(check reference 3 and 5 in case of doubt)*
- It means that when a script is run, the JS engine runs the code line by line, beginning at the top and working its way down. 
- As a result, the JavaScript engine only has **one call stack** and can only perform one action at a time.
<hr/>

### Relation between Execution Context and Call Stack-
* When the execution of the JavaScript code starts, a **Global Execution context** is created and pushed onto the Call Stack. This Global Execution context can be seen in your Chrome browser in the form of the `window` object and in Node.js we can find the same in the form of the `global` object.
* Every function, once called for execution, generates an execution context that then gets **pushed to the top** of the call stack thus getting in line to get the access to all the resources (variables, functions, objects) required for its execution.
* After the execution of all the functions in the code is complete, the Global Execution context is also **popped off** the call-stack.
![Call Stack](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ibhnjcpmp3nal6g6gsnd.png)
*Credits- [Danny Zhang](http://dannyzhang.run/2017/04/03/How-JavaScript-works-Behind-the-Scenes/)*

### 3 Types of Execution Context-

**1) Global Execution Context-**

* It is the base or the default execution context. Any code that is not present inside any function is said to be inside the Global Execution context that is why we are able to access them using the `window` object.
* It also provides us with the `this` keyword to help reference the `window` object.
* Create a memory heap in order to store variables and function references.
* Stores all the function declarations in the memory heap and the variables in the **Global Execution context** with its initial values as `undefined`.
![Global Execution Context illustration](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/94w9ouc5e42wyf27rvwn.png)
*Credits- [Lexical](https://whynotgoogleit.com/javascript-execution-stack-and-hoisting/)*

**2) Functional Execution Context-**

* These are created for every function call thus, unlike Global Contexts, we can have multiple Functional Execution contexts.
* They can access all the code of the Global Context but the Global Context cannot access the code of the **Functional Execution context**.


**3) Eval Execution Context-**

* Any code executed via the `eval` function has its own executional context.

### Creating an Execution Context-

**1) Creation Phase-**
  * *Task 1- Creation of Activation/ Variable object*

   * The activation object is like a memory unit/ **container** 
  for storing the variables, objects etc related to a function.
  
  * *Task 2- Creation of Scope Chain*

    * Scope chain is the list of variables and objects created 
    within a particular function.
    * Once the **scope chain** is formed, it helps initialize 
    value of `this`.

**2) Execution Phase-**
  * The JS engines scan over the function in the code one more 
  time, updating the variable object with the values of the 
  variables and then running the code.

### What is Stack Overflow/ Call Stack Overflow:
* Stack overflow occurs when the call stack becomes full/ can fit no more function calls or contexts.
* This may occur when a recursive function is run with **no exit** point and the function exceeds the storage limit of the call stack.
* Storage of the call stack is dependent on the host environment, the web browser or the Node.js env.
![Stack Overflow code](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2wh5i29mvt40wxk1h3tm.png)
[Open Code in JS Fiddle](https://jsfiddle.net/mkzt8fa2/) 

<hr/>
## Appendix-

1. [**Advanced JavaScript Series - Part 1**: Behind the scenes (JavaScript Engine, ATS, Hidden Classes, Garbage Collection)](https://dev.to/pranav016/advanced-javascript-series-part-1-behind-the-scenes-javascript-engine-ats-hidden-classes-garbage-collection-3ajj)
1. [**Advanced JavaScript Series - Part 2**: Execution Context and Call Stack](https://dev.to/pranav016/advanced-javascript-series-part-1-execution-context-and-call-stack-l1o)
<hr/>

#### References-

1. https://www.javatpoint.com/javascript-execution-context
2. https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts/?utm_source=udemy&utm_medium=coursecontent#call-stack-memory-heap
3. https://www.javatpoint.com/javascript-call-stack
4. https://medium.com/@alexandrawilll/javascript-execution-context-call-stack-and-event-queue-d58b672d76f7#:~:text=Every%20line%20of%20code%20in%20JS%20has%20an%20execution%20context.&text=When%20a%20function%20executes%2C%20an,off%20of%20the%20call%20stack.
5. https://stackoverflow.com/questions/16523870/is-javascript-synchronousblocking-or-asynchronousnonblocking-by-default