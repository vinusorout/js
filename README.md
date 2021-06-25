Personal learning

# Async Await

```js
// mark the main function async to use await:
const loaddata = async () => {
  const url = "url";
  const res = await fetch(url);
  const data = await res.json();
  return data;
}
loaddata().then(data => console.log(data));

// you cant use await at top-level Await (with out function)
// Immediately Invoked Function (IIFE pronounced as IIFY)
// for this use IIFE, below fuction is IIFE and will execute
( () => {
})();
// async IIFE
( async () => {
  const data = await loaddata();
  console.log(data);
})();

// Top level await is available in Node.js since 14.8
// top-level await is only available in ES modules. (the import statement instead of require)

// first way to ES
// to make a js file as ES script rename the file as .mjs (stands for module JavaScript)
// index.mjs, this top level await will work with command node index.mjs
import got from 'got'; // im mjs file import work not require
const data = await got('url').json();
console.log(data);

// second way to ES
// keep file as index.js, and in package.json file "type": "module"

// Promise.all, let say in index.js with ES
const url2 = "url2";
const url3 = "url3";
const result = await Promise.all([
  fetch(url2),
  fetch(url3)
]);
const dataPromises = results.map(result => result.json())
const finalData = await Promise.all(dataPromises);
console.log(finalData);
```

# Equality
## The == and === is only applicable for primitive types (int, string etc), not for objects for object every language match refrence data
```js
// ==
"1" == 1 // It convert the both side of data in same type before comparison

// ===
"1" === 1 // doesnt convert and result is false

// objects
const obj1 = {
  name: '1'
}

const obj2 = {
  name: '1'
}

const obj3 = obj2;

console.log(obj1==obj2) // False
console.log(obj1===obj2) // False

console.log(obj3==obj2) // True
console.log(obj3===obj2) // True

```

# Some ES6 or ES2015 highlights
## let vs var
Variables that are declared with the var keyword in the global scope are added to the window/global object. Therefore, they can be accessed using window.variableName.

Whereas, the variables declared with the let keyword are not added to the global object, therefore, trying to access such variables using window.variableName results in an error.

## Arrow functions

```js
var arrowAdd = (a,b) => a + b;
```

## Classes

```js
/ Before ES6 version, using constructor functions
function Student(name,rollNumber,grade,section){
  this.name = name;
  this.rollNumber = rollNumber;
  this.grade = grade;
  this.section = section;
}

// Way to add methods to a constructor function
Student.prototype.getDetails = function(){
  return 'Name: ${this.name}, Roll no: ${this.rollNumber}, Grade: ${this.grade}, Section:${this.section}';
}


let student1 = new Student("Vivek", 354, "6th", "A");
student1.getDetails();
// Returns Name: Vivek, Roll no:354, Grade: 6th, Section:A

// ES6 version classes
class Student{
  constructor(name,rollNumber,grade,section){
    this.name = name;
    this.rollNumber = rollNumber;
    this.grade = grade;
    this.section = section;
  }

  // Methods can be directly added inside the class
  getDetails(){
    return 'Name: ${this.name}, Roll no: ${this.rollNumber}, Grade:${this.grade}, Section:${this.section}';
  }
}

let student2 = new Student("Garry", 673, "7th", "C");
student2.getDetails();
// Returns Name: Garry, Roll no:673, Grade: 7th, Section:C
```

## Destructuring properties
```js
var person = {
  name: 'vinay',
  lastname: 'sorout'
}
var {lastName} = person;

const classDetails = {
  strength: 78,
  benches: 39,
  blackBoard:1
}

const {strength:classStrength, benches:classBenches,blackBoard:classBlackBoard} = classDetails;

console.log(classStrength); // Outputs 78
console.log(classBenches); // Outputs 39
console.log(classBlackBoard); // Outputs 1
```

## Spread Operator(three dots ...)
### usefull to make copy of arrays, objects
```js
  var arr1 = [1,2,3]
  var arr2 = [...arr1, ...arr2]
  
  // Copy objects
  const food = {a: 'a', b: 'b'};
  const newFood = {...food}
  
  // other ways to copy object
  // "Object.assign"
  Object.assign({}, food)

  // other ways to copy object
  // "JSON"
  JSON.parse(JSON.stringify(food))
  
```

## backtick allows using variable in string
```js
 const a = 'a';
 console.log(`value of a is ${a}`);
```

## Arrays methods (Filter, Some, Map, reduce, every)
### Filter
```js
  const array1 = [
  { name: 'a', height: 10 },
  { name: 'b', height: 12 },
  { name: 'c', height: 08 },
  ];
  const array2 = array1.filter( (item) => {
    return item.height >= 10;
  });
```

### Map, iterate through each item of array, we can update the array and the result will be a NEW ARRAY
```js
  const array1 = [
  { name: 'a', height: 10, width: 10 },
  { name: 'b', height: 12, width: 11  },
  { name: 'c', height: 08, width: 12 },
  ];
  // return only name of each object
  const names = array1.map( (item) => {
    return item.name;
  });
  const namesandheights = array1.map( (item) => {
    return {name: item.name, height: item.heigh };
  });
  console.log(namesandheights) // [{name:'a', height: 12}, {name:'b', height: 10}, {name:'c', height: 08}]
```

### Some, altest one item meet with the condition
```js
  const array1 = [
  { name: 'a', height: 10 },
  { name: 'b', height: 12 },
  { name: 'c', height: 08 },
  ];
  const isTrue = array1.some( (item) => {
    return item.height >= 10;
  });
  console.log(isTrue); // True
```

### Sort
```js
  const array1 = [
  { name: 'a', height: 10 },
  { name: 'b', height: 12 },
  { name: 'c', height: 08 },
  ];
  const sortedArray = array1.sort( (item1, item2) => {
    // if return is negative then item 1 is sorterd before item 2
    // if return is positive then item 2 is sorted before item 1
    // if return 0 then equal
    return item1.height - item2.height;
  });
  console.log(sortedArray);
  
  const sortedArrayWithString = array1.sort( (item1, item2) => {
    // if return is negative then item 1 is sorterd before item 2
    // if return is positive then item 2 is sorted before item 1
    // if return 0 then equal
    if(item1.name < item2.name) return -1;
    return 1;
  });
  console.log(sortedArrayWithString);
```

### Reduce, when you iterate through the array items and in the end want some ending result, for ex sum of height
```js
  const array1 = [
  { name: 'a', height: 10, eyeColor: 'red' },
  { name: 'bb', height: 12, eyeColor: 'red'  },
  { name: 'c', height: 08, eyeColor: 'blue'  },
  ];
  const sumOfheight = array1.reduce( (accumilator, currentItem) => {
    return accumilator + currentItem.height; // the accumilator value will be 0, passed in next line
  }, 0); // initial value of accumilator
  console.log(sumOfheight); // 30
  // IMPORTANT
  const noOfCharactersByEyeColors = array1.reduce( (accumilator, currentItem) => {
    if(accumilator[currentItem.eyeColor]) {
      accumilator[currentItem.eyeColor]++;
    } else {
      accumilator[currentItem.eyeColor] = 1;
    }
    return accumilator;
  }, {}); // initial value as empty object for accumilator
  console.log(noOfCharactersByEyeColors); // {red: 2, blue: 1}
  
  // find total number of charcters in names of array
  const totalNameCharcters = array1.reduce( (accumilator, currentItem) => accumilator + currentItem.name.length, 0);
  console.log(totalNameCharcters) // 4
```


### Every, each item should match the condition only then True otherwise Fasle
```js
  const array1 = [
  { name: 'a', height: 10 },
  { name: 'b', height: 12 },
  { name: 'c', height: 08 },
  ];
  const isTrue = array1.every( (item) => {
    return item.height >= 10;
  });
  console.log(isTrue); // False
```


## JAVASCRIPT IMP QUESTIONS

### JavaScript is a dynamically typed language. In a dynamically typed language, the type of a variable is checked during run-time

### Implicit Type Coercion
```js
// Implicit Type Coercion in javascript
var x = 3;
var y ="3"
console.log(x + y); // 33 String coercion takes place while using the ‘ + ‘ operator. When a number is added to a string, the number type is always converted to the string type

console.log(x - y); // 0 Type coercion also takes place when using the ‘ - ‘ operator, but the difference while using ‘ - ‘ operator is that, a string is converted to a number and then subtraction takes place
```

### Javascript Closures
Closures is an ability of a function to remember the variables and functions that are declared in its outer scope.

```js
function randomFunc(){
  var obj1 = {name:"Vivian", age:45};

  return function(){
    console.log(obj1.name + " is "+ "awesome"); // Has access to obj1 even when the randomFunc function is executed

  }
}

var initialiseClosure = randomFunc(); // Returns a function

initialiseClosure(); 
```

Let’s understand the code above,
The function randomFunc() gets executed and returns a function when we assign it to a variable:

```js
var initialiseClosure = randomFunc();
```

The returned function is then executed when we invoke initialiseClosure:

```js
initialiseClosure(); 
```

The line of code above outputs “Vivian is awesome” and this is possible because of closure.
When the function randomFunc() runs, it sees that the returning function is using the variable obj1 inside it:

```js
console.log(obj1.name + " is "+ "awesome");
```
Therefore randomFunc(), instead of destroying the value of obj1 after execution, saves the value in the memory for further reference. This is the reason why the returning function is able to use the variable declared in the outer scope even after the function is already executed.

**This ability of a function to store a variable for further reference even after it is executed, is called Closure.**

### Javascript Constructor Functions for objects
Constructor functions are used to create objects in javascript.

```js
function Person(name,age,gender){
  this.name = name;
  this.age = age;
  this.gender = gender;
}


var person1 = new Person("Vivek", 76, "male");
console.log(person1);

var person2 = new Person("Courtney", 34, "female");
console.log(person2);
```


