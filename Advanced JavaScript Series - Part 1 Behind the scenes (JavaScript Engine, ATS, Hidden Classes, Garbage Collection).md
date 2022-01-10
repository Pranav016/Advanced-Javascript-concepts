## Introduction-

JavaScript is a single-threaded, synchronous programming language. It means that when a script is run, the JS engine runs the code line by line, beginning at the top and working its way down.

## Behind the scenes-

![Flowchart1](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tb8ol66g9infpetxsgiz.png)
_Credits- [Yair Cohen](https://coralogix.com/blog/how-js-works-behind-the-scenes%E2%80%8A-%E2%80%8Athe-engine/)_

### 1. JavaScript Engine

![Flowchart2](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/94ww1vgzutji2qoke4q7.png)
_Credits- [Yair Cohen](https://coralogix.com/blog/how-js-works-behind-the-scenes%E2%80%8A-%E2%80%8Athe-engine/)_

-   Every JavaScript program requires a specific environment to execute because our computers and other machines do not understand JavaScript syntax.
-   They only understand _[Machine Code](https://en.wikipedia.org/wiki/Machine_code)_ thus every environment has an engine that converts this JS human understandable syntax to Machine Code.
-   There are many different engines available out there with the most popular being the Google Chrome's V8 engine, Firefox SpiderMonkey, JavaScriptCore by Safari etc.
-   **[ECMAScript](https://en.wikipedia.org/wiki/ECMAScript)** is a JavaScript standard that helps ensure interoperability of JS web pages by keeping a check on how all the different engines interpret the JavaScript language.

### 2. Parser/ Syntax Parser

![Flowchart3](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/s42zl32gr7x5oraf5mqm.png)
_Credits- [Yair Cohen](https://coralogix.com/blog/how-js-works-behind-the-scenes%E2%80%8A-%E2%80%8Athe-engine/)_

-   Every JS engine has a parser in it which knows all the JS syntax rules and checks for any syntax or grammar errors.
-   If found, it gives out an error otherwise the Parser generates an **Abstract Syntax Tree** that is then passed on to aid the code execution.

### 3. Abstract Syntax Tree (AST)

![Flowchart4](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/74js34tooi6v63t1hftr.png)
_Credits- [Yair Cohen](https://coralogix.com/blog/how-js-works-behind-the-scenes%E2%80%8A-%E2%80%8Athe-engine/)_

-   It is a tree like structural representation of the JS code.
-   The main purpose for creating an AST is that it helps understand the code better and helps make the translation to machine code much easier.
-   You can see how an AST is formed & represented on [AST Explorer](https://astexplorer.net/).

### 4. Interpreter

![Flowchart5](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ht9ofhqklm5lifq7y1au.png)
_Credits- [Yair Cohen](https://coralogix.com/blog/how-js-works-behind-the-scenes%E2%80%8A-%E2%80%8Athe-engine/)_

-   The interpreter takes the AST and parses and transform it into an **[Intermediate Representation](https://en.wikipedia.org/wiki/Intermediate_representation#:~:text=An%20intermediate%20representation%20%28IR%29%20is,such%20as%20optimization%20and%20translation.)**.

#### Intermediate Representation-

-   Intermediate Representation acts as an intermediate step between translation from an abstract language such as JS to machine code.
-   The most famous Intermediate representation amongst JS engines is **[Bytecode](https://en.wikipedia.org/wiki/Bytecode)**.
    ![IR](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/y5y78aw418qng2k8zszi.png)
    _Credits- [Satyabrata Jena](https://auth.geeksforgeeks.org/user/Satyabrata_Jena/articles)_

##### Need for Intermediate Representation(IR)-

1. Unlike Machine code that are hardware dependent, IRs are universal thus allowing more mobility and easier conversions.
1. It is easier to optimize code when it is in IR than it being in machine code.

### 5. Compiler

![Flowchart6](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/10jk02xso6zdd34mehpx.png)
_Credits- [Yair Cohen](https://coralogix.com/blog/how-js-works-behind-the-scenes%E2%80%8A-%E2%80%8Athe-engine/)_

-   The main purpose of a compiler is to take the Intermediate representation received from the previous step, perform optimizations and then convert it to Machine code.

### Difference between Interpreter and a Compiler

-   An interpreter and a compiler are different in the way that an interpreter translates your code and runs it line by line, whereas a compiler instantaneously converts all code into machine code before executing it.
-   Each has advantages and disadvantages; a **compiler is quick but complex** and difficult to start, whereas an **interpreter is slower but simpler**.
-   With that in mind, there are **three methods for converting high-level code to machine code** and running it:

1. **Interpretation** – this technique uses an interpreter to go through the code line by line and execute it (not so efficient).
1. **Ahead of Time Compilation (AOT)** - entails a compiler first compiling and then executing the complete code.
1. **Just-In-Time Compilation (JIT)** — A hybrid of the AOT and interpretation strategies, a JIT compilation approach aims to combine the best of both worlds by performing dynamic compilation while also allowing for optimizations, resulting in a compilation process that is significantly sped up.

-   A JIT compiler is used by the majority of JS engines, although not all of them.
-   Checkout this [article](https://coralogix.com/blog/how-js-works-behind-the-scenes%E2%80%8A-%E2%80%8Athe-engine/) for a more complete explanation on the topic.

## Extras-

### 1. Hidden Classes

-   As we all know, JavaScript is a dynamic programming language.
-   While this is a benefit of JavaScript's dynamic nature, it also has a disadvantage. In memory, JS objects are stored in what is known as a **HASH TABLE**. When compared to the contiguous buffer method used in non-dynamic programming languages, retrieving a property on an object with hash tables is substantially slower.
-   Hidden classes, a mechanism provided by the V8 engine, gives the answer. **Hidden classes** are used to reduce the time it takes to retrieve a property from an object. This is **accomplished by sharing hidden classes across similar-looking objects.**
    When a JavaScript object is created, a hidden class is assigned to it.
-   The length of an offset to reach the hidden class can easily be determined based on the property’s type, whereas this is not possible in JavaScript where a property’s type can change **during runtime**.
-   Hidden Classes are attached at **runtime**.
-   When a property is introduced to an object, a **"class transition"** occurs, in which the previous hidden class is replaced by a new hidden class that includes the new property. Let's look at an example to help you understand.

```
function cupcake(frosting,sprinkles) {
    this.frosting = frosting;
    this.sprinkles = sprinkles;
}
```

-   We have a constructor function cupcake that takes as argument the frosting type and the sprinkles type and whenever this function is invoked; we get an object that is our new Cupcake!
-   V8 creates a hidden class called Class0 when it sees our cupcake function is declared. When V8 notices that frosting has been added as a property on the cupcake on line 2, it changes class0 with the new frosting property and switches from class0 to a new hidden class called class1. The same happens when sprinkles are added to the cupcake and class transition occurs from class1 to class2.
-   Checkout this [article](https://medium.com/swlh/writing-optimized-code-in-js-by-understanding-hidden-classes-3dd42862ad1d) for a more in-depth explanation on hidden classes.

### 2. Inline Caching

-   **Inline caching** relies upon the observation that repeated calls to the same method tend to occur on the same type of object. [2]
-   V8 keeps a cache of the types of objects that have been **supplied as parameters** in recent method calls and uses that data to guess what type of object will be passed as a parameter in the future.
-   If **V8** can make a good guess about the type of object that will be provided to a method, it can skip the process of finding out how to access the object's properties and instead **rely on previously stored** information from lookups to the hidden class.
    ![Objects](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b485rs95wr3sn6lzhfap.png)
    _Credits- [Yair Cohen](https://coralogix.com/blog/how-js-works-behind-the-scenes%E2%80%8A-%E2%80%8Athe-engine/)_

#### Relation between Hidden classes and Inline caching

-   When a method on a specific object is called, the **V8 engine** must look up the hidden class of that object to calculate the offset for accessing a specific attribute. V8 skips the hidden class lookup after two successful calls to the same hidden class and simply adds the offset of the property to the object pointer itself. The V8 engine thinks that the **hidden class** hasn't changed for all subsequent calls to that method, and leaps directly into the memory address for a given field using offsets recorded from prior lookups, considerably **increasing execution performance**.
-   The importance of objects of the same type **sharing hidden classes** is due to inline caching. V8 will not be able to use **inline caching** if you create two objects of the same type but with different hidden classes (as we did in the previous example). This is because, despite the fact that the two objects are of the same type, their corresponding hidden classes assign different offsets to their properties.
-   JS being **dynamically typed**, occasionally the hidden class assumption about the object might be wrong. In that case V8 goes for the original call that is searching from the Hash Table that makes the data fetching slower.

#### Optimizations to take advantage of Hidden Classes and Inline Caching-

-   Try to assign all properties of an object in its constructor.
-   If still(for some reason), you are dynamically adding new properties to the objects, always instantiate them in the **SAME ORDER so that hidden classes may be shared** among them because then the V8 engine is able to predict them thus assigning the same hidden class to both the objects.
-   Below is an example of a good and a bad practice for this use case-

##### Bad Practice-

```
1  function Point(x,y) {
2    this.x = x;
3    this.y = y;
4  }
5
7  var obj1 = new Point(1,2);
8  var obj2 = new Point(3,4);
9
10 obj1.a = 5;
11 obj1.b = 10;
12
13 obj2.b = 10;
14 obj2.a = 5;
```

Up until line 9, obj1 and obj2 shared the same hidden class. However, since properties a and b were added in opposite orders, obj1 and obj2 end up with different hidden classes.

##### Good Practice-

```
1  function Point(x,y) {
2    this.x = x;
3    this.y = y;
4  }
5
7  var obj1 = new Point(1,2);
8  var obj2 = new Point(3,4);
9
10 obj1.a = 5;
11 obj2.a = 5;
12
13 obj1.b = 10;
14 obj2.b = 10;
```

### 3. Garbage Collection

-   JavaScript is a **Garbage collected language**.
-   Meaning that if we allocate some memory inside a function, JavaScript will automatically deallocate that memory once the function finishes executing or is out of scope.
-   But the issue of **[Memory Leak](https://en.wikipedia.org/wiki/Memory_leak)** still prevails in JS like in other languages. Thus it is important to ensure good memory management on our part.
-   JS collects garbage with a **[mark and sweep](https://www.geeksforgeeks.org/mark-and-sweep-garbage-collection-algorithm/)** method.
![Mark and sweep](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qiq0w2a6uuhz8lrvoaae.png)
_Credits- [Andrei Neagoie](https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts/?utm_source=udemy&utm_medium=coursecontent#call-stack-memory-heap)_
<hr/>

![Code](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i71muydk6hy8toeuj4rw.png)
_[Open code in JS Fiddle](https://jsfiddle.net/j7569dfh/)_

-   In this example, a **memory leak** is created. By changing the value of `person`, we leave the previous value in the memory heap thus causing a leak.
-   Best practice against memory leaks are to avoid global instantiation, instead we should instantiate only inside functions, where required.
<hr/>

## Appendix-

1. [**Advanced JavaScript Series - Part 1**: Behind the scenes (JavaScript Engine, ATS, Hidden Classes, Garbage Collection)](https://dev.to/pranav016/advanced-javascript-series-part-1-behind-the-scenes-javascript-engine-ats-hidden-classes-garbage-collection-3ajj)
1. [**Advanced JavaScript Series - Part 2**: Execution Context and Call Stack](https://dev.to/pranav016/advanced-javascript-series-part-1-execution-context-and-call-stack-l1o)
 <hr/>

## References-

1. https://coralogix.com/blog/how-js-works-behind-the-scenes%E2%80%8A-%E2%80%8Athe-engine/
1. https://richardartoul.github.io/jekyll/update/2015/04/26/hidden-classes.html
1. https://www.geeksforgeeks.org/difference-between-source-code-and-byte-code/
1. https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts/?utm_source=udemy&utm_medium=coursecontent#call-stack-memory-heap
1. https://medium.com/swlh/writing-optimized-code-in-js-by-understanding-hidden-classes-3dd42862ad1d
