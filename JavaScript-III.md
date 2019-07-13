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

### Constructor Function Examples

Example 1

```
function Animal(object) { // We pass every constructor an object
  this.name = object.name;   // The this keyword gets returned as the new object
}
```

Example 2

```
function Person(attributes) {
  this.age = attributes.age;
  this.name = attributes.name;
  this.homeTown = attributes.homeTown;
  this.speak = function() {
    return `Hello, my name is ${this.name}.`;
    }
  };
  
  const fred = new Person({ 
    age: 32,
    name: "Fred",
    homeTown: "Bedrock"
});

console.log(fred);  // Prints: Person {age: 32, name: "Fred", homeTown: "Bedrock", speak: ƒ}
fred.speak();  // Prints: "Hello, my name is Fred."
```

## The Object Prototype

1. The mechanism by which all objectscan inherit properties from one another
2. Allows one to "deliberately" modify an object's properties
3. Helps to avoid memory problems
4. Allows one to extend an object's properties to another object.
5. Can be *VERY DANGEROUS*. You can overwrite an entire object's methods!

Example

```
function Person(attributes) {
  this.age = attributes.age;
  this.name = attributes.name;
  this.homeTown = attributes.homeTown;
  };
  
  Person.prototype.speak = function() {
    return `Hello, my name is ${this.name}.`;
  };
  
  const liz = new Person({ 
    age: 38,
    name: "Liz Lemon",
    homeTown: "Manhattan"
});

console.log(liz);  // Prints: Person {age: 28, name: "Liz Lemon", homeTown: "Manhattan"}
liz.speak();  // Prints: "Hello, my name is Liz Lemon."
```

## Prototypal Inheritance (Child)

```
function Child(childAttributes) { 
  Person.call(this, childAttributes); // binding the this keyword to Person
  this.isChild = childAttributes.isChild; // special attribute to Child
 }
 
 Child.prototype = Object.create(Person.prototype); // Child.prototype to make EXACTLY like the Original/Parent
 
 const pebbles = new Child({ 
   age: 3,
   name: "Pebbles",
   homeTown: "Bedrock"
  });
  
  // NOTE: Because of the Child.prototype above, we can invoke speak() from fred
  
  pebbles.speak(); // Prints "Hello, my name is Pebbles"
```





