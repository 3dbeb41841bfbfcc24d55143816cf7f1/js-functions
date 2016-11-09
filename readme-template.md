# JavaScript Functions

{{TOC}}

## What are the objectives?

*After this lesson, developers will be able to:*

* **Describe** why functions are created
* **Use** functions to break programs into smaller sub-programs
* **Describe** how parameters relate to functions
* **Explain** what scope is
* **Compare** global and local scope
* **Describe** the `this` keyword and how it is affected by scope

## Why are Functions Important?

* Keep your code **DRY** - functions allow us to *reuse* the same block of code
* **Abstraction** - functions allow us to define a problem and solve it in an encapsulated way
* **Testability** - because functions are well-defined, they are easy to test for correctness
* **Libraries** - Another form of reuse, we can use JavaScript libraries to contain functions we plan to use over and over

## Functions in Mathematics:

![alt tag](https://raw.githubusercontent.com/ATL-WDI-Curriculum/js-functions/master/images/function_math.png)

Given a simple function

    y = f(x)

if we let f(x) = x^2
then we have:

    f(2) = 4
    f(3) = 9
    etc.

In Mathematics, functions have inputs, outputs, a name, and a definition.

It is similar in Computer Science.

## Declaring a JavaScript Function

```javascript
// syntax for declaring a function
function <function_name>(arguments) {
   <function_body>
}
```

### Example #1

> Note: we can try out this function in [repl.it](https://repl.it/languages/javascript)

```javascript
// function declaration 
function square(x) { 
  return x * x; 
}
 
// calling the function
var y = square(3);
console.log("y = " + y);  // will print "y = 9"
```

## Definition

> A ***function*** is a sequence of program instructions that perform a specific task, packaged as a unit. This unit can then be used in programs wherever that particular task should be performed.

Functions provide:

* Reuse
* Abstraction
* Testability

### Example #2

```javascript
// find the average of two numbers 
function average(x, y) {
  return (x + y) / 2; 
}

 // calling the function 
var y = average(20, 40); 
console.log("y = " + y);  // will print "y = 30"
```

## The Return Statement

The ***return*** statement ends the execution of the function and (optionally) returns a value to the caller.

### Example #3

```javascript
// return the first object in the array that has the specified id.
function findById(arr, id) {
  for (var i = 0; i < arr.length; i++) {
    if (arr[i].id === id) {
      return arr[i];
    }
  }
  return null;      // why do we need this?
}
```

### Example #4

```javascript
// calculate income tax
function getTax(income) {
  if (income < 50000) {
    return income * 0.15;
  }
  else if (income < 100000) {
    return income * 0.20;
  }
  else {
    return income * 0.25;
  }
}

// calling the function
console.log("Tax on 40000 = " + getTax(40000));
console.log("Tax on 80000 = " + getTax(80000));
console.log("Tax on 120000 = " + getTax(120000));
```

## When There Is No Return Statement

Not all functions have a return value.

### Examples

```javascript
line(10, 20, 60, 100); // draws a line
console.log(str);      // outputs str to console
```

Since a function is called to perform some task, the function must either (a) ***return*** a value; or (b) ***change**** the environment in some way; or (c) ***both***.

### Pure Functions

Functions that do *not* change the environment (and thus only return a value) are called ***pure*** functions.

Pure functions are generally easier to reason about and test because they are ***deterministic*** (i.e. predictable).

Pure functions also provide for easier ***composition***.

![alt tag](https://raw.githubusercontent.com/ATL-WDI-Curriculum/js-functions/master/images/composite-function.png)

One of the primary characteristics of ***Functional Programming*** is that most or all of the functions are ***pure*** functions.

### Functions in Variables

JavaScript can store anything in variables.

> Including functions!

### More Function Declarations

```javascript
// simple function declaration 
function square(x) {
  return x * x;
}

// function assigned to a variable
 var square = function(x) {
  return x * x;
};

// functions as properties of an Object 
var mathHelpers = { 
  square: function(x) {
    return x * x;
  },
  average: function(x, y) { 
    return (x + y) / 2; 
  }
 };

// invoking a "method"
var y = mathHelpers.square(3);
```

## Functions as 1st Class Citizens

In computer science, a programming language is said to have ***first-class*** functions if it treats functions as first-class citizens.

Specifically, this means that the language supports:

* Assigning functions to variables
* Storing functions within data structures
* Passing functions as arguments to other functions
* Returning functions as the value from other functions

### Example #5

```javascript
// TODO:
```

## Anonymous Functions

```javascript
function foo() {
  // This is a named function...
}

function() {
  // This is an anonymous function...
}
```

Common uses of anonymous functions:

* store it as an object key’s value
* store it in a variable inside an object
* pass it as an argument to a function or method
  - use it as a callback or handler

## Functions & Scope

In modern programming languages, variables have a ***scope***, i.e. the part of the program where a variable is bound to a memory location. You can think of the ***scope*** as the lifetime of the variable (where in the program the variable is born and where it dies or is discarded).

***Global*** variables have ***global*** scope; they are alive for the entire duration of the program execution.

***Local*** variables have ***local*** scope; they are alive during a part of the execution of the program.

> For JavaScript (before JavaScript 2015), local variables are scoped by their enclosing ```function```.  JavaScript 2015 is introducing ***lexical*** scope for variables declared with the `let` keyword.

### Example #6

```javascript
var president = "Everyone knows me. Globally!";

function town() {
  var mayor = "I'm unknown outside of my township.";

  function house() {
    var homebody = "No one knows me. " +
      "I don't leave home. " +
      "but I know the mayor and the president.";
  }

  evilDictator = "I am evil! Want to know why?";
}
```

> If you forget the `var` keyword when declaring / introducing a new variable, JavaScript will ***punish*** you by making the variable ***global***. Many JavaScript **linters** (static code analyzers) will detect and report this mistake.

## Functions: Hoisting

JavaScript will allow you to declare new variables anywhere in your code, but the declarations are ***hoisted*** to the top of the enclosing function during execution.

### Example #7

```javascript
// What we wrote
function add(x, y) {
  x = x || 0;
  y = y || 0;
  var sum = x + y;
  return sum;
}

// What gets executed
function add(x, y) {
  var sum;
  x = x || 0;
  y = y || 0;
  sum = x + y;
  return sum;
}
```

Note that only the *declaration* gets hoisted, not the assignment to a value.
