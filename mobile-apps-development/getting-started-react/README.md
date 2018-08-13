# Getting Started React

Sebelum memulai ke React. Mari kita bahas tentang ES6 \(EcmaScript 2015\). ES6 adalah fitur bahasa pada pemrograman Javascript modern.

## Daftar Fitur ES6

* Arrows Function
* Classes
* Enchanced object literals
* Template strings
* Destructuring
* Default + rest + spread
* Let + const
* Iterators + for..of
* Generators
* Unicode
* Modules
* Modules loaders
* Map +set + weakmap + weakset
* Proxies
* Symbols
* Subclassable built-ins
* Promises
* Math + number + string + array + object apis
* Binary dan octal literals
* Reflect API
* Tail calls

Tidak perlu menguasai seluruh fitur diatas. Diharuskan menguasai 8 fitur, diantaranya :

1. Let + Const
2. Arrow Functions
3. Default Parameters
4. Destructuring
5. Rest Parameters + Spread Operator
6. Enhanced object literals
7. Template literals
8. Promises

### Let + Const

```javascript
var x = 1;

if (x === 1) {
var x = 2;

console.log(x);
// expected output: 2
}

console.log(x); // 2
```

```javascript
let x = 1;

if (x === 1) {
  let x = 2;

  console.log(x);
  // expected output: 2
}

console.log(x); // 1
```

```javascript
const number = 42;
number = 100; // Uncaught TypeError: Assignment to constant variable.
```

### Arrow Functions

Normal Javascript:

```javascript
function f (){
    // isi Function
}

var f = function(){
    // isi function
}
```

ES6 :

```javascript
var f = () => {
    //function
    return () => {
        //returning function
    }
}
```

### Default Parameters

```javascript
function multiply(a, b = 1) {
  return a * b;
}

console.log(multiply(5, 2));
// expected output: 10

console.log(multiply(5));
// expected output: 5
```

### Destructuring

Normal Javascript:

```javascript
let studentName = {
    firstName: 'Peter',
    lastName: 'Parker'
};

const firstName = studentName.firstName;
const lastName = studentName.lastName;
```

ES6:

```javascript
let studentName = {
    firstName: 'Peter',
    lastName: 'Parker'
};

const { firstName, lastName } = studentName;

console.log(firstName); // Peter
console.log(lastName); // Parker
```

## Rest Parameters + Spread Operator

```javascript
// Rest Parameters

let scores = ['98', '95', '93', '90', '87', '85']
let [first, second, third, ...restOfScores] = scores;

console.log(first) // 98
console.log(second) // 95
console.log(third) // 93
console.log(restOfScores) // [90, 87, 85]
```

```javascript
let array1 = ['one', 'two']
let array2 = ['three', 'four']
let array3 = ['five', 'six']

// ES5 Way / Normal Javascript

var combinedArray = array1.concat(array2).concat(array3)
console.log(combinedArray) // ['one', 'two', 'three', 'four', 'five', 'six']

// ES6 Way 

let combinedArray = [...array1, ...array2, ...array3]
console.log(combinedArray) // ['one', 'two', 'three', 'four', 'five', 'six']
```

## Enhanced object literals

```javascript
const fullName = 'Zell Liew'

const Zell = {
  fullName: fullName
}

// ES6 way
const Zell = {
  fullName
}
```

## Template Literals

```javascript
const firstName = 'Zell'
const lastName = 'Liew'
const teamName = 'unaffiliated'

const theString = `${firstName} ${lastName}, ${teamName}`

console.log(theString)
```

