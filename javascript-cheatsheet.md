### Object
```javascript
// simple object
var o = {firstName: "steve", lastName: "Liu"}

// create object - method 1
var mango = {
    color: "yellow",
    getColor: function() {
        return this.color;
    }
}

// create object - method 2
var mango = new Object();
mango.color = "yellow";
mango.getColor = function() { return this.color; }

// object constructor - method 1.
function Fruit(name, color) {
    this.name = name;
    this.color = color;
    this.getName = function() { return this.name; }
    this.getColor = function() { return this.color; }
}
var mango = new Fruit("mango", "yellow");

// object constructor - method 2
function Fruit() {}
Fruit.prototype.name = "mango";
Fruit.prototype.color = "yellow";
Fruit.prototype.getName = function() { return this.name; };
Fruit.prototype.getColor = function() { return this.color; };
```

### In/hasOwnProperty
```javascript
// `in` also check the parent's poverty
var school = { schoolName:"MIT" }
console.log("schoolName" in school);                // true​
​console.log("schoolType" in school);                // false​
​console.log("toString" in school);                  // true

// `hasOwnProperty` check only current object
var school = {schoolName:"MIT"};                    
​console.log(school.hasOwnProperty ("schoolName"));  // true​
​console.log(school.hasOwnProperty ("toString"));    // false
```

### Prototype
```javascript
// inheritance
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

### Closure
```javascript
// 1. inner function can access outer function's variables.
// 2. the outer function must be called.

// Closures have access to the outer function’s variable even after the outer function returns.
function show() {
    var intro = "Your name is ";
    function showName(name) {
        return intro + name;
    }
    return showName;
}
var info = show();
info("Steve");

// Closures store references to the outer function’s variables.
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
id.getID();         // 1213
id.setID(6666);     // 6666
id.getID();         // 6666

// Closures Gone Away (because Closures stores reference).
``` 


### This
```javascript
// 1. The property `this` is a variable with the value of the object that invokes the function where this is used.
// 2. The `this` inside function is not assigned a value until an object call the function.

// `this` refer to window.
var firstName = "Peter", lastName = "Ally";
function showFullName () { console.log (this.firstName + " " + this.lastName); }
showFullName();         // Peter Ally​

// this is refer to $("button"), so cannot read property '0' of undefined
$ ("button").click (user.clickHandler); 
$ ("button").click (user.clickHandler.bind(user)); // solution

// this inside the anonymous function cannot access the outer function’s this. 
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
// Solution: use `that`.
var user = {
  tournament:"The Masters",
  data:["T. Woods", "P. Mickelson"],
  clickHandler:function () {
    var that = this;
    this.data.forEach (function (name) {
        console.log (name + " is playing at " + that.tournament);
    })
  }
}
```

### bind/apply/call
```javascript
// bind - function.bind(thisArgv, argv1, argv2, ...)
this.x = 9;
var o = { x: 81, getX: function() { return this.x; }};
var getGlobalX = module.getX;
getGlobalX();                       // 9
var getBoundX = getGlobalX.bind(o);
getBoundX();                        // 81

// bind - partial function
function list() { return Array.prototype.slice.call(arguments); }
var leadingThirtysevenList = list.bind(null, 37);
var list2 = leadingThirtysevenList();               // [37]
var list3 = leadingThirtysevenList(1, 2, 3);        // [37, 1, 2, 3]

// call - function.call(thisArgv, argv1, argv2, ...)
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

// apply: function.call(thisArg, [argv, argv2, ...])
```

### Immediately-Invoked Function Expression (IIFE)
```javascript
(function(){ /* code */ }()); 
(function(){ /* code */ })(); 
```

### Inheritance
```javascript
// http://js-bits.blogspot.com/2010/08/javascript-inheritance-done-right.html
function extend(base, sub) {

  function surrogateCtor() {}
  // Copy the prototype from the base to setup inheritance
  surrogateCtor.prototype = base.prototype;
  // Tricky huh?
  sub.prototype = new surrogateCtor();
  // The constructor property is set wrong (to the base constructor)
  // with the above trick, let's fix it
  sub.prototype.constructor = sub;
}
```

### Module
```javascript

```