# JavaScript III

## The Four Principles of `this`

1. During Global Binding, the value of `this` will be the Window/Console Object. For example,
 the console output will have `Window {postMessage: f, blur: f, ...}`.
2. Whenever a function is called by a preceding dot `.`, the object to the left of the dot gets
`this`.
3. Whenever a constructor function is used, `this` refers to the specific instance of the object
that is created and returned by the constructor function.
4. Whenever JavaScript's `.call()` or `.apply()` method is used, `this` is explicitly defined.

## Global Binding
* When in the global scope, the value of `this` will be the Window/console Object

```
function sayName(name) {
  console.log(this);  // prints Window {postMessage: f, blur: f, ...}
  return name;
  }
```  

## Implicit Binding

* Whenever a function is called by a preceding dot, the object to the left of the dot gets `this`.

```
const myObj = {
 greeting: "Hello",
 sayHello: function(name) {  // sayHello is considered a method
   console.log(`${this.greeting}, my name is ${name}`);
   console.log(this);  // the `this` points to the myObj variable at the top of this block of code
   }
 };
 myObj.sayHello("Ryan")
 ```
 
 ## New Binding
 
 * Whenever a constructor function is used, `this` refers to the specific instance of the object that 
 is created and returned by the constructor function
 
 ```
 function CordialPerson(greeter) {   // CordialPerson is the Constructor function
   this.greeting = "Hello";
   this.greeter = greeter;
   this.speak = function() {
     console.log(this.greeting + " " + this.greeter);
     console.log(this); // after jerry.speak prints, the global will print: 
   }                    // CordialPerson {greeting: "Hello", greeter: "Newman", speak: ƒ}
 };
 
const jerry = new CordialPerson("Newman");
const newman = new CordialPerson("Jerry");

jerry.speak();  // prints Hello Newman
newman.speak(); // prints Hello Jerry
```

## Explicit Binding

* Whenever JavaScript's call() or apply() methods are used, `this` is explicitly defined. 

```
 function CordialPerson(greeter) {   // CordialPerson is the Constructor function
   this.greeting = "Hello";
   this.greeter = greeter;
   this.speak = function() {
     console.log(this.greeting + " " + this.greeter);
     console.log(this); // after jerry.speak.call(newman) prints, the global will print: 
   }                    // CordialPerson {greeting: "Hello", greeter: "Jerry", speak: ƒ}
 };
 
const jerry = new CordialPerson("Newman");
const newman = new CordialPerson("Jerry");

jerry.speak.call(newman);  // prints Hello Jerry
newman.speak.apply(jerry); // prints Hello Newman
```

## Object Oriented Programming (OOP)

1. Objects over functions
2. Data over logic
3. A logical procedure that takes in input data, processes it and returns it as an output.
4. JavaScript is *NOT* a class-based language by nature.
5. Classes in JavaScript are what's called "Syntactic Sugar" over the constructor pattern.
6. We have pseudo-classical inheritance (and a few others) that we can use to achieve Object Oriented Programming.

## Constructor Functions

1. Constructors are also known as Object Creator Functions
2. Sole purpose of Constructor functions is to take in some sort of input, create an object *and* return an object out of that input.
3. By convention, these are Capitalized Functions. For example, `function Person()`.
4. Instantiated with the `new` keyword. Meaning, it creates a new object.
5. `this` becomes the object which will be returned by `new`.
