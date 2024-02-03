# javaScriptInterviewQuiz

💥💥💥var, let, const💥💥💥

🔑 SCOPE
var is **functional scope**
let is **block scope**
const is **block scope**

**functionalScope**
function example() {
  if (true) {
    var x = 10;
    console.log(x); // Output: 10
  }
  console.log(x); // Output: 10
}

**blockScope**
function example() {
  if (true) {
    let y = 20;
    console.log(y); // Output: 20
  }

🔑 HOIST
var = Hoisted to the top of its scope and initialized with undefined.
let = Hoisted to the top of its block but not initialized until the declaration statement is executed.
const = Hoisted to the top of its block but not initialized until the declaration statement is executed.

**var hoist**
console.log(a); // Output: undefined (hoisted but not initialized yet)
var a = 5;
console.log(a); // Output: 5

**let hoist**
// console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;
console.log(b); // Output: 10

**const hoist**
// console.log(c); // ReferenceError: Cannot access 'c' before initialization
const c = 15;
console.log(c); // Output: 15

**functions hoist**
Function declarations are hoisted along with their entire bodies, allowing you to call a function before its declaration in the code.

sayHello(); // Output: Hello!
function sayHello() {
  console.log('Hello!');
}

However, function expressions (where a function is assigned to a variable) are not hoisted in the same way.
// This would result in an error
sayHi(); // TypeError: sayHi is not a function
var sayHi = function() {
  console.log('Hi!');
};

🔑 REASSIGNED AND REDECLARED
var = Can be both reassigned and redeclared within the same scope.
let = Can be reassigned within the same block but cannot be redeclared in the same scope.
const = Cannot be reassigned after initialization. For objects and arrays, **properties or elements can still be modified** (shallow immutability).

**const with object and array can modified**
**object**
const person = { name: 'John', age: 25 };
person.age = 26; // Allowed (shallow immutability)

**array**
const numbers = [1, 2, 3];
numbers[0] = 10; // Allowed (shallow immutability)


💥💥💥Describe the concept of closures💥💥💥

# Before you learn about closures, you need to understand two concepts:
1️⃣ **Nested Function**
2️⃣ **Returning a function**

1️⃣ **JavaScript Nested Function**
In JavaScript, a function can also contain another function. This is called a nested function. For example,

// outer function
function greet(name) {

    // inner function
    function displayName() {
        console.log('Hi' + ' ' + name);
    }

    // calling inner function
    displayName();
}

// calling outer function
greet('John'); // Hi John

2️⃣ **Returning a function**
function greet(name) {
    function displayName() {
        console.log('Hi' + ' ' + name);
    }

    // returning a function
    return displayName;
}

const g1 = greet('John');
console.log(g1); // returns the function definition
g1(); // calling the function

In the above program, the greet() function is returning the displayName function definition.

👆 Here, the returned function definition is assigned to the g1 variable. When you print g1 using console.log(g1), you will get the function definition.
To call the function stored in the g1 variable, we use g1() with parentheses.

👍 **JavaScript Closures** 👍
A closure allows a function to remember and access variables from its outer (enclosing) scope even after the outer function has finished executing.

function outerFunction() {
    // Outer function's variable
    let outerVariable = "I am from the outer function";

    // Inner function (closure)
    function innerFunction() {
        console.log(outerVariable);
    }

    // Returning the inner function
    return innerFunction;
}

// Assigning the returned function (closure) to a variable
const closureExample = outerFunction();

// Calling the closure, which still has access to outerVariable
closureExample(); // Output: I am from the outer function
