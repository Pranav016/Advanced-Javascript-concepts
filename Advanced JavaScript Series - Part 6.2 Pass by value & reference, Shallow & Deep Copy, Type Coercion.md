## Pass by Value-

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

-   Objects are always passed by refernce.

### Example-

#### Code-

```
let obj1={
  a: 'a',
  b: 'b',
  c: 'c'
}

let obj2={...obj1} //one way of copying the object
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

-   But this is only a shallow copy of the original object. Lets understand this with the help of an example.

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

-   The problem with shallow copy is that, if the user makes changes to the complex object (update street property of address object) of the source object (userName), it is also reflected in the Destination Object, since it points to the same memory address and vice-versa.

-   Thus we turn towards Deep Copying. Deep copying means that value of the new variable is disconnected from the original variable while a shallow copy means that some values are still connected to the original variable.

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
let obj2=JSON.parse(JSON.stringify(obj1))
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
    d: "d"
  }
}
```

-   Here we can see that changes made in `obj2` are not reflected in `obj1` thus we can say that its a deep copy and the two objects are disconnected.

### How to compare two objects having different memory location but same value-

[Article](https://stackoverflow.com/questions/1068834/object-comparison-in-javascript)

`JSON.stringify(obj1) === JSON.stringify(obj2)`

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

//Guess the outputs
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

## Type Coercion
