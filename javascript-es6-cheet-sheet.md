### var, let, const
```javascript
// let cannot be re-declared.
// const cannot be re-assigned.
```

### Arrow function
```javascript
// implicit return
const count_double = (x) => x * 2;

// skip `that = this;`
function myFunc() {
  this.myVar = 0;
  setTimeout(() => {
    this.myVar++;
    console.log(this.myVar) // 1
  }, 0);
} 
```

### Default Parameter
```javascript
// no parameter provided or undefined parameter provided
function myFunc(x = 10) {
  return x;
}
```

### Destructuring Objects
```javascript
// fetch object properties
const person = {
  firstName: "Nick",
  lastName: "Anderson",
  age: 35,
  sex: "M"
}
const { age } = person;

// passing person
function joinFirstLastName({ firstName, lastName }) {
  return firstName + '-' + lastName;
}

// destructuring 
const myArray = ["a", "b", "c"];
const [x, y] = myArray; // x is "a", y is "b"
```

### map/filter/reduce
```javascript
const numbers = [0, 1, 2, 3, 4, 5, 6];

// map
const doubledNumbers = numbers.map(n => n * 2); // [0, 2, 4, 6, 8, 10, 12]

// filter
const evenNumbers = numbers.filter(n => n % 2 === 0); // [0, 2, 4, 6]

// reduce
const sum = numbers.reduce((prev, next) => prev + next, 0); // 21
```

### Spread Operator
```javascript
const arr1 = ["a", "b", "c"];
const arr2 = [...arr1, "d", "e", "f"]; // ["a", "b", "c", "d", "e", "f"]

const { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
console.log(x); // 1
console.log(y); // 2
console.log(z); // { a: 3, b: 4 }
``` 

### Promise
```javascript
const fetchingPosts = new Promise((res, rej) => {
  $.get("/posts")
    .done(posts => res(posts))
    .fail(err => rej(err));
});

fetchingPosts
  .then(posts => console.log(posts))
  .catch(err => console.log(err));
```

### String Template
```javascript
const condiment = "jam";
const meal = "toast";
highlight`I like ${condiment} on ${meal}.`;

const snacks = ['apples', 'bananas', 'cherries'];
comma`I like ${snacks} to snack on.`;
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










