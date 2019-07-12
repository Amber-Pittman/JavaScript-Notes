# JavaScript-Notes
Notes I took during my JavaScript lectures at Lambda School


# JavaScript IV

JavaScript Classes

1. The `class` keyword is what we call "syntactic sugar." Meaning, it's an abstactor on top of Constructor Functions.
2. It's all Constructors and Prototypes under the hood (the dev tools console of your web browser).
3. This is *NOT* a new Object-Oriented inheritance model in JavaScript.
4. You've already learned how JavaScript classes work by way of learning Constructor Functions and about the Prototype Object. 
5. Classes in JavaScript are special Functions.
6. We will learn about Class declarations.


## Set Up a Class:

```
class Rectangle {
  constructor (height, width) {
    this.height = height;
    this.width = width;
   }
}


const newRect = new Rectangle(400, 800);
console.log(newRect);  // prints Rectangle {height: 400, width: 800}
```



* The constructor function is the glue that binds this all together. Anything you need as direct properties on your class will be done through `constructor( )`. That is built a built-in method that comes "out of the box."
* `Parent.call(this, attrs)` is something we never have to do again.


*Inheritance with Classes*
1. The `extends` will abstract away the `.call(this, attrs)`
2. The `super( )` function will abstract away any of the funky syntax that we have been using to bind our Object's prototypes to one another.
3. This syntax is awesome because it is declarative and obvious which class inherits from which. 
4. #### Classes are just functions.


*How to Extend a Class:*

```
// PARENT    
class Animal {
  constructor(name) {
    this.name = name;
   }
speak() {     // speak() is a method
  console.log(this.name + " makes a noise.");
  }
}


// Extend Animal to a Dog Class


// CHILD
class Dog extends Animal {
  constructor(name) {
    super(name);  // Super takes care of the binding with `.call()`
  }    // Super grants access to the parent! You need it if you want to use Animal's method, `speak()`
speak() {
  console.log(this.name + " barks.");
  }
}
```



#### Important to Know:


The `speak( )` method we declared inside the class is NOT going to be a property on the Dog Object. However, it is going to be a property method on the prototype of the Animal's instantiated object.


Examples:

```
// PARENT    
class Animal {
  constructor(name) {
    this.name = name;
   }
speak() {     
  console.log(`${this.name} says, "Hello.");
  }
} 


const wilson = new Animal("Wilson");
console.log(wilson)  // prints Object { name: "Wilson"}




// Extend the PARENT!!!




// CHILD
class Dog extends Animal {
  constructor(name) {
    super(name);  
  }               
}


const bowWow = new Dog("Dublin");
console.log(bowWow);


bowWow.speak();  // prints Dublin says Hello.
```

HOWEVER, since the `bowWow.speak( )` gave us a human response, we need to add a speak method in the Child Object. Update the Child in the previous code to this:

```
// CHILD
class Dog extends Animal {
  constructor(name) {
    super(name);  
  }
  speak() {
    console.log(`${this.name} barks!`);               
}


const bowWow = new Dog("Dublin");
console.log(bowWow);


bowWow.speak();  // prints Dublin barks!
```



Here is a second Child Object.

```
class Cat extends Animal {
  constructor(name) {
    super(name);
  }
speak() {
  console.log(`${this.name} meows!`);
  }
}


const kitty = new Cat("Pepper");
console.log(kitty)


kitty.speak(); // prints Pepper meows!
```



## Converting Constructors into Classes
1. Classes are just Constructor Functions
2. Classes are easy to use
3. Inheritance is trivial to set up
4. Classes call for cleaner code
5. We get the Prototype system for free


Example:

```
// PARENT    


function Person(attrs) {
  this.age = attrs.age;
  this.name = attrs.name;
  this.homeTown = attrs.homeTown;
}


Person.prototype.speak = function() {
  return `Hello, my name is ${this.name}.`;
};




//  CONVERT TO CLASS


class Person {          // Notice function is replaced with class and no need for attrs on this line
  this.age = attrs.age;
  this.name = attrs.name;
  this.homeTown = attrs.homeTown;
}
speak() {              // Object.prototype.() is no longer necessary here
  return `Hello, my name is ${this.name}.`;
  }
};
```

Inheritance Example (Child):

```
function Child(childAttrs) {
  Person.call(this, childAttrs;
  this.isChild = childAttrs.isChild;
}


Child.prototype.checkIfChild = function() {
  if(this.isChild) {
    console.log(`${this.speak} and I am a child Object.`);
  }
};




// CONVERT TO CLASS


class Child extends Parent {
  constructor(childAttrs) {
    super(childAttrs);  // `super` is the "special sauce". It calls the Parent constructor.
    this.isChild = childAttrs.isChild;  // Special child attributes AFTER inheriting parental attributes
  }
  checkIfChild() {
    if(this.isChild) {
      console.log(`${this.speak} and I am a child object.`);
  }
};
```





#### MORE Examples (Fruit Constructors to Classes - view on  https://codepen.io/lambdaschool/pen/JeELbw?editors=0011)

```
// PARENT
class Fruit {
 constructor(attrs) {
   this.type = attrs.type;
   this.name = attrs.name;
   this.isRipe = attrs.isRipe;
   this.calories = attrs.calories;
}
shipped(destination) {
  console.log(`Shipping ${this.name} to ${destination}.`);
}
calculateCals() {
  console.log(`Calories in ${this.name} are ${this.calories * 200}.);
  }
};




// CHILD
class Banana extends Fruit {
  constructor(bananaAttrs) {
    super(bananaAttrs);
    this.doMonkeysLikeIt = bananaAttrs.doMonkeysLikeIt;
}
checkIfMonkeysLikeIt() {
  if(this.doMonkeysLikeIt) {
    return true;
  } else {
    return false;
  }
 }
};




// SECOND CHILD
class Kiwi extends Fruit {   // Using `extends` allows Kiwi to inherit Fruit attributes
  constructor(kiwiAttrs) {
    super(kiwiAttrs);
    this.isFuzzy = kiwiAttrs.isFuzzy;
  }
checkIsFuzzy() {
  if(this.isFuzzy) {
    return true;
  } else {
    return false;
  }
 }
};




// fruit variables
const newBanana = new Banana({
  doMonkeysLikeIt = true,
  type = tree,
  name = "Banana",
  isRipe = false,
  calories = 0.1
  });
console.log(newBanana);




const newKiwi = new Kiwi({
  isFuzzy = true,
  type = "Tree",
  name = "Kiwi",
  isRipe = false,
  calories = 0.7
});
console.log(newKiwi);
```

