## Execution Context

Global execution context (`this` equal to `window`) is created default by JavaScript engine.  
Global means not inside function.  
Two phase in Execution Context:
1. Creation phase: setup up memory for `functions` and `variables`.
2. Execution phase: execute the code line by line.

## Hoisting

The `console.log(a)` will raise `undefined`, but the function `b()` will print the string `Hello World`.   
When the javascript engine create the Execution context, they setup memory space for variables and functions. The 
whole `functions` are placed into memory, but the `variables` are placed into memory ans set `undefined`.  
All JavaScript variables are set `undefined` by default.

```javascript
console.log(a);
b();

var a = "Hello World";
function b() {
  console.log("Good luck");
}
```

## Not Defined & Undefined

The `not defined` means the variable is never declared and `undefined` means variable declared but not assigned. 

## Function, Variables, Execution Context

First, the `llobal execution context` created. When we hit `a()`, a new execution context will be created and be pushed
to `execution context stack`. When `b()` run, new execution context is created. Whenever any function finish, the 
execution context will be popped from stack. The variable `a` will run on each `execution context`.
Every function will create NEW `execution context` and be placed into the stack.

```javascript
function a() { b(); var a = "Hello"; }
function b() { var a = 10; }
a();
var a;
```

## Scope Chain

The `execution context` will resolve the variables by `outer environment` which use `lexcical positision`. The 
`lexcical positision` is the physical position where the function truly at.

In this example, the `outer environment` of `b()` is `global execution context`. 

```javascript
function b() {
    console.log(hi);  // print `1`
}
function a() {
    var hi = 2;
    b();
}
var hi = 1;
a();
```

In this example, the `outer environment` of `b()` is `a()` and the `outer environment` of `a()` is `global`.

```javascript
function a() {
    function b() {
        console.log(hi) // print `1`
    }
    b();
}
var hi = 1;
a();
```

## Event Queue & Execution Context Stack

Events will be placed into `event queue`, and ONLY when `execution context stack` is empty.

## Primitive Types

Never use `undefined` and use `null` for not existence.

Javascript will do automatically transfer during `==`, so we have to to use strict equal `===`. Strict equal will also
check the data type.

```javascript
Number(undefined);  // print `NaN`
Number(null);       // print `0`

"3" == 3            // print `true`
"3" === 3           // print `false`
```

How to set default value?

```javascript
function greeting(s) {
    var fname = s || "default";
}
```

## Object

You can create object by `new object()` or object literals `{}`.

```javascript
var person = new Object();
var person = {};
```

All `functions` are `objects`. First class functions: Everything you can do with other types you can do with functions. 

```javascript
function greeting() {
    console.log("hi");
}
greeting.userName = "Hello World";
```

How to set anonymous function?

```javascript
var anonymousGreeting = function() {    
    console.log("Greeting");
}
```


## Prototype

Every object has a property called `proto {}`.

In prototype chain, `this.xxxx` will search through above prototype to find the corresponding values.

```
Obj1 ---> Proto {} --> Proto {}
          ^ 
         /
Obj2 ---/
```

Inheritance in prototype.

```javascript
function Plant() {
    this.country = "Taiwan";
    this.organic = true;
    this.getCountry = function() { return this.country; }
    this.getOrganic = function() { return this.organic; }
}
function Fruit(name, color) {
    this.name = name;
    this.color = color;
    this.getName = function() { return this.name; }
    this.getColor = function() { return this.color; }
}

// inheriting all of Plant.prototype methods and properties.​
Fruit.prototype = new Plant();

// fix the broken connection
Fruit.prototype.constructor = Fruit;
```

Create a object and inherit person's properties as prototype by `Object.create()` and set the object prototype 
to `person` object. 

```javascript
var person = {
    firstName: "Default",
    lastName: "Default"
}
var john = Object.create(person);   // john is empty object and its prototype have all properties of person
```

Jane and John's prototype refer to the `person` object.

```javascript
var person = {
  name: "hello"
}

var john = Object.create(person);
var jane = Object.create(person);

person.name = "world";

console.log(john.name);     // print `world`
console.log(jane.name);     // print `world` because their prototype refer to person
```

How does `Object.create()` implement in plain javascript ?

```javascript
if (!Object.create) {
  Object.create = function (o) {
    if (arguments.length > 1) {
      throw new Error('Object.create implementation'
      + ' only accepts the first parameter.');
    }
    function F() {}
    F.prototype = o;
    return new F();
  };
}
```

## New Operator

Construct a new object by `var john = new Person()`. The `new` will create a empty object and then invoke the function,
so the `this` in person will refer to the empty object.

```javascript
function Person() {
    this.firstName = "John";
    this.lastName = "Doe";
}

var john = new Person();
```

When a person is created, it's prototype will refer `Person.prototype`.

```javascript
function Person() {
    this.firstName = "John";
    this.lastName = "Doe";
}

Person.prototype.getFullName = function() {
    return this.firstName + this.lastName;
}

var john = new Person();
var jane = new Person();
```

Often you will see `variables` sits inside `object` and `method` stays in the `prototype`.

- More efficient if you have a thousand objects and all the methods refer to prototype.

## This

1. The property `this` is a variable with the value of the object that invokes the function where this is used.
2. The `this` inside function is not assigned a value until an object call the function.

```javascript
function a() {
    console.log(this);
    this.newVar = "hello";
}
a();    // when function `a()` invoke, `this` will be assign to `window` object.
```

Use `that` to avoid `this` assignment errors.
```javascript
var c = {
    name: "The c object",
    log: function() {
        var that = this;    //  always use `that` will be assign to current object, so you do not have to worry about anything.
        that.name = "Updated c object";     
    }
}
```

The `this` refer to window.
```javascript
var firstName = "Peter", lastName = "Ally";
function showFullName () { console.log (this.firstName + " " + this.lastName); }
showFullName();         // Peter Ally​
```

The `this` is refer to `$("button")`, so cannot read property '0' of undefined.

```javascript
$ ("button").click (user.clickHandler); 
$ ("button").click (user.clickHandler.bind(user)); // solution
```

The `this` inside the anonymous function cannot access the outer function’s this. 

```javascript
var user = {
  tournament:"The Masters",
  data:["T. Woods", "P. Mickelson"],
  clickHandler:function () {
    this.data.forEach (function (name) {
        console.log (name + " is playing at " + this.tournament);
    })
  }
}
user.clickHandler();        // What is "this" referring to? [object Window]


var user = {
  tournament:"The Masters",
  data:["T. Woods", "P. Mickelson"],
  clickHandler:function () {
    var that = this;      // Solution: use `that`.
    this.data.forEach (function (name) {
        console.log (name + " is playing at " + that.tournament);
    })
  }
}
```

## Immediately-Invoked Function Expression (IIFE)

```javascript
(function(){ /* code */ }()); 
(function(){ /* code */ })(); 
```

`IIFE` will make sure that variables will stay in each `execution context` and not pollute each other.

```javascript
var greeting = "global hello";      // create in `global execution context`
(function(window) {
    var greeting = "IIFE hello";    // create in `new execution context`
})(window);                         // pass global object to IIFE
console.log(greeting);              // print `global greeting`
```

## Closure

When function `show()` is called, it create a new `show execution context`. When function `show()` return, the
`show execution context` is popped from the stack, but the variable is still in the memory. The function `showName()` still can refer
to the `show() execution context` because of `scope chain`.

- The inner function can access outer function's variables.
- The outer function must be called

```javascript
function show() {
    var intro = "Your name is ";
    function showName(name) {
        return intro + name;
    }
    return showName;
}
var info = show();
info("Steve");
```

```javascript
function ID() {
    var id = 1213;
    return {
        getID: function() {
          return id;
        },
        setID: function(new_id) {
          id = new_id;
        }
    }
}
var id = ID();
id.getID();         // print `1213`
id.setID(6666);     // set `6666`
id.getID();         // print `6666`
``` 

## Bind & Apply & Call

`bind` - function.bind(thisArgv, argv1, argv2, ...)

```javascript
this.x = 9;
var o = { x: 81, getX: function() { return this.x; }};
var getGlobalX = module.getX;
getGlobalX();                       // 9
var getBoundX = getGlobalX.bind(o);
getBoundX();                        // 81
```

`bind` as partial function

```javascript
function list() { return Array.prototype.slice.call(arguments); }
var leadingThirtysevenList = list.bind(null, 37);
var list2 = leadingThirtysevenList();               // [37]
var list3 = leadingThirtysevenList(1, 2, 3);        // [37, 1, 2, 3]
```

`call`: function.call(thisArgv, argv1, argv2, ...)
`apply`:  function.call(thisArg, [argv, argv2, ...])

```javascript
function greet() {
  var reply = [this.person, 'Is An Awesome', this.role].join(' ');
  console.log(reply);
}
var p = { person: 'Douglas Crockford', role: 'Javascript Developer' };
greet.call(p); 

// call - chain constructor
function Product(name, price) {
  this.name = name;
  this.price = price;
}
function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

// call - without thisArgv
var sData = 'Wisen';
function display() { console.log('sData value is %s ', this.sData); }
display.call();

```

## in & hasOwnProperty

The `in` also check the prototype's poverty.

```javascript
var school = { schoolName:"MIT" }
console.log("schoolName" in school);                // true​
​console.log("schoolType" in school);                // false​
​console.log("toString" in school);                  // true
```

The `hasOwnProperty` check only current object.

```javascript
var school = {schoolName:"MIT"};                    
​console.log(school.hasOwnProperty ("schoolName"));  // true​
​console.log(school.hasOwnProperty ("toString"));    // false
```

## strict mode

In strict mode, we have to always declare variables.

```javascript
"use strict";
person = {}     // this throw errors.
```

## 10 things learn from jQuery

[10 things learn from jQuery](https://www.youtube.com/watch?v=i_qE1iAmjFg)

## Module

A simple module. You can refer to `Javascript: Understandning the WeridParts`;

```javascript
(function (window, document, undefined) {
  
    var Greetr = function(name) {
        return new Greetr.init(name);
    }

    // methods can put here in `Greetr.prototype`
    
    Greetr.prototype = {};
    
    Greetr.init = function(name) {
        var that = this;        // always use that, then you dont have to worry.   
        that.name = name;
    }
    
    window.Greetr = window.G$ = Greetr; 
    
})(window, document, undefined);
```