## ES6

[Modern Javascript Tutorial](https://javascript.info)  
[ES5 vs ES6](http://es6-features.org/#Constants)

## ECMAScript

ECMAScript is the standard. JavaScript is the implementation. ES 2015 is equal to ES6.

```
ES6 Code --> Babel --> ES5 Code 
```

## forEach

Iterate through the array.

```ecmascript 6
var colors = ["javascript", "blue", "green"];
colors.forEach(function(corlor) {
    console.log(corlor);
})
```

## map

Iterate through array and return new elements into array.

```ecmascript 6
var numbers = [1, 2, 3];
var double = numbers.map(function (number) { 
    return number * 2;    
});
console.log(double);        // print `[2, 4, 6]`
```

## filter

`filter` use true as condition to create new object and append to array.

```ecmascript 6
var fruits = [{type: "v"}];
var filterFruits = fruits.filter(function(fruit) {
	return fruit.type === "v";
});
console.log(filterFruits)       // print `[{type: "v"}]`
```

## find

`find` will return the first match object.

```ecmascript 6
var users = [{name: "Alex"}, {name: "Steve"}];
var findUser = users.filter(function(user) {
	return user.name === "Steve";
});
console.log(findUser)
```

### every & some

`every` will make sure that every are true.

`some` if only one of object is true, then it is true.


```ecmascript 6
var computers = [
    {type: "mac", ram: 16},
    {type: "windows", ram: 8},
    {type: "linux", ram: 32},
]

computers.every(function(computer) {
    return computer.ram > 10;
});     // `false` because not every computer's ram greater than 10g


computers.some(function(computer) {
    return computer.ram > 10;  
});     // `true` because some computer's ram greater than 10g
```

### reduce

`reduce` will take one start arg and deal with the value in the array.

```ecmascript 6
var numbers = [1, 2, 3, 4, 5];
numbers.reduce(function(previous, number) {
    return previous + number;
}, 0);      // print `15`
```

```ecmascript 6
var colors = [{color: "red"}, {color: "blue"}, {color: "yellow"}];
colors.reduce(function(previous, color) {
    return previous + color.color;
}, []);      // print ["red", "blue", "yellow"]
```

## const & let & var

`let` can't be re-declared and use to replace `var`.

`const` can't be re-assigned.

```ecmascript 6
let i = 10;
const array = [1, 2, 3];
```

### String Template

`${}` inside \`\` will be treated as JavaScript expression.

```ecmascript 6
const condiment = "jam";
const meal = "toast";
console.log(`I like ${condiment} on ${meal}.`);

const snacks = ['apples', 'bananas', 'cherries'];
console.log(`I like ${snacks[0]} to snack on.`);
```

### Arrow Function

As an implicit return or directly use return.

```ecmascript 6
const count_double = (x) => x * 2;

const count_double = (x) => {
    return x * 2;
}
```

No argument you have still to put parenthesis.

```ecmascript 6
const count_double = () => 1000;
```

Arrow function does not has his own context, `this` will refer to the inherited function context (We don't have to bind).

```ecmascript 6
function Button(){ 
    this.num = 100; 
    this.click = () => {
      this.num += 1;
      console.log(this.num);
    };
} 
let btn = new Button();
let fn = btn.click;
fn()    // print `101`
```

If arrow function is defined in object, it will  refer to some other function context (we need `bind` or `that = this`).

```ecmascript 6
var button = {
    num: 100,
    click: () => {
        this.num += 1;
    }
};
var fn = btn.button;
fn();
```

## Enhanced Object Literal

If you have the same key and value, you can just pass `key` name;

```ecmascript 6
let url = "https://www.google.com";

let data = {url, method: "post"};
```

## Default Parameter

No parameter provided or undefined parameter provided.

```ecmascript 6
function myFunc(x = 10) {
  return x;
}
myFunc();
```

## Rest & Spread operator

Unpack the array into elements.

```ecmascript 6
const arr1 = ["a", "b", "c"];
const arr2 = [...arr1, "d", "e", "f"]; // ["a", "b", "c", "d", "e", "f"]
```

Compact elements into map or array.

```ecmascript 6
const { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
console.log(x);     // 1
console.log(y);     // 2
console.log(z);     // { a: 3, b: 4 }
```

## Destructuring Objects

Create a const reference to the properties.

```ecmascript 6
const person = {
  firstName: "Nick",
  lastName: "Anderson",
  age: 35,
  sex: "M"
}
const { age, sex } = person;
```

Destruct arguments object.

```ecmascript 6
const person = {
  firstName: "Nick",
  lastName: "Anderson",
  age: 35,
  sex: "M"
}
function joinFirstLastName({ firstName, lastName }) {
  return firstName + '-' + lastName;
}
joinFirstLastName(person);
```

Destruct array.

```ecmascript 6
const myArray = ["a", "b", "c", "d"];
const [x, y] = myArray;             // x is "a", y is "b"
const [x, y, ...rest] = myArray;    // x is "a", y is "b", rest is ["c", "d"]
```

Destruct object in array.

```ecmascript 6
const companies = [
    {name: "Google", location: "Mountain View"},
    {name: "Facebook", location: "Menlo Park"}
]
const [{googleLocation}] = companies;       // Mountain View
```

Destruct array in object.

```ecmascript 6
const Google = {
    locations: ["Mountain View", "New York", "London"]
}
const { locations: [location] } = Google;
console.log(location);      // Mountain View
```


































### Promise
```javascript
const fetchingPosts = new Promise((resolve, reject) => {
  setTimeout(() => {
    if (Math.random() % 2 === 1) { resolve('Sucess'); }
    else { reject("Failure"); }
  }, 1000);
});

// put 2 callbacks into then()
fetchingPosts.then((res) => {
  console.log(res);
}, (err) => {
  console.log(err);
});

// put to then() and catch()
fetchingPosts.then((res) => {
  console.log(res);
}).catch((err) => {
  console.log(err);
});
```

### Imports/Export
```javascript
// basic exports
// mathConstants.js
export const pi = 3.14;
export const exp = 2.7;
export const alpha = 0.35;

// -------------

// myFile.js
import { pi, exp } from './mathConstants.js'; // Named import -- destructuring-like syntax
console.log(pi) // 3.14
console.log(exp) // 2.7

// -------------

// mySecondFile.js
import * as constants from './mathConstants.js'; // Inject all exported values into constants variable
console.log(constants.pi) // 3.14
console.log(constants.exp) // 2.7

// default imports
// coolNumber.js
const ultimateNumber = 42;
export default ultimateNumber;

// ------------

// myFile.js
import number from './coolNumber.js';
// Default export, independently from its name, is automatically injected into number variable;
console.log(number) // 42
```

### Class
```javascript
// before ES6
var Person = function(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.stringSentence = function() {
  return "Hello, my name is " + this.name + " and I'm " + this.age;
}

// after ES6
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  stringSentence() {
    return "Hello, my name is " + this.name + " and I'm " + this.age;
  }
}

// super
// 1. super keyword must be used before the this keyword is used in constructor
// 2. If the parent class have a method called X, you can use super.X() to call it in a child class.
class Polygon {
  constructor(height, width) {
    this.name = 'Polygon';
    this.height = height;
    this.width = width;
  }
  getHelloPhrase() {
    return `Hi, I am a ${this.name}`;
  }
}
class Square extends Polygon {
  constructor(length) {
    super(length, length);
    this.name = 'Square';
    this.length = length;
  }
  getCustomHelloPhrase() {
    const polygonPhrase = super.getHelloPhrase(); // accessing parent method with super.X() syntax
    return `${polygonPhrase} with a length of ${this.length}`;
  }
  get area() {
    return this.height * this.width;
  }
}
```

### Async Await
```javascript
// await must be used in an async function
async function getGithubUser(username) { 
  const response = await fetch(`https://api.github.com/users/${username}`); 
  return response.json();
}
getGithubUser('mbeaudru').then(user => console.log(user)).catch(err => console.log(err));

// chain async/await
async function getUser() { // The returned promise will be rejected!
  throw "User not found !";
}
async function getAvatarByUsername(userId) => {
  const user = await getUser(userId);
  return user.avatar;
}
async function getUserAvatar(username) {
  var avatar = await getAvatarByUsername(username);
  return { username, avatar };
}
getUserAvatar('mbeaudru')
  .then(res => console.log(res))
  .catch(err => console.log(err)); // "User not found !"

// chain await
async function fetchPostById(postId) {
  const token = (await fetch('token_url')).json().token;
  const post = (await fetch(`/posts/${postId}?token=${token}`)).json();
  const author = (await fetch(`/users/${post.authorId}`)).json();
  post.author = author;
  return post;
}

fetchPostById('gzIrzeo64')
  .then(post => console.log(post))
  .catch(err => console.log(err));
```

### Generator
```ecmascript 6
// Basics
function *gen() {
  yield "1";
  yield "2";
  yield "3";
}
var g = gen();
g.next(); // {value: 1, done: false}


// pass parameters to next
// 1. Pass the parameter to next().
// 2. suspend at yield and wait for next next() called.

function *gen(s) {
  
  let second_next_pass_parameter = yield "1st yield, " + s;
  console.log(second_next_pass_parameter);
  
  let third_next_pass_parameter = yield "2nd yield, " + s;
  console.log(third_next_pass_parameter);
  
  let fourth_next_pass_parameter = yield "3rd yield, " + s;
  console.log(fourth_next_pass_parameter);
  
}
var g = gen('Hello');
console.log(g.next('This will not be pass'));
console.log(g.next('This is 2nd next'));
console.log(g.next('This is 3rd next'));
console.log(g.next('This is 4th next'));
```

### static
```javascript
class Repo{
  static getName() {
    return "Repo name is modern-js-cheatsheet"
  }
}

//Note that we did not have to create an instance of the Repo class
console.log(Repo.getName()) 

//Uncaught TypeError: repo.getName is not a function
let r = new Repo();
console.log(r.getName()) 
```

### get & set
```javascript
const numbers = {
    arr: [1, 2, 3], 
    get firstNinja(){
      console.log("get index 0");
      return this.arr[0];
    },
    set firstNinja(value){
      console.log("set index 0");
      this.arr[0] = value;
  }
};

numbers.firstNinja // get index 0
numbers.firstNinja = 100 // set index 0
```
