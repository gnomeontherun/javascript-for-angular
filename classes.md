# Classes

* [What are classes?](#what-are-classes)
* [Basic syntax](#basic-syntax)
* [A class as ES5](#a-class-as-es5)
* [Constructor method](#constructor-method)
* `this`[ and classes](#this-and-classes)
* [Static methods](#static-methods)
* Extending classes
* Mixins
* Role of classes in Angular
  * Component and Directive Controllers
  * Services
  * Pipes

* Best practices
* Things to avoid
* [Resources](#resources)

## What are classes?

Classes are a new way to define an object in JavaScript. They are only a new syntax to create objects, and do not directly introduce new concepts into the language itself. They are often referred to as **syntactic sugar** because it can make it easier to define and express objects.

Here is a quick look at a simple class.

```js
class Calculator {
  constructor() {
    this.clear();
  }

  add(a) {
    this.result += a;
  }

  clear() {
    this.result = 0;
  }
}
```

This basic class sets up a new object called `Calculator`, adds two methods to its prototype \(`add()` and `clear()`\), defines a property \(`result`\), and runs the constructor method when a new instance is initialized.

When you use a class to create an object, it is fundamentally a function object. You would not use a class to define a new string or number object for instance.

You can define any number of properties and methods \(technically just a property that happens to be a function\) for a class. These properties can be set during object creation, using a constructor method to initialize the object, or can be modified after creation.

An object created with a class still uses prototypes. A new class will define a new prototype based on the properties and methods declared. Classes can extend another class, which will link the prototype of the class to the parent prototype.

Classes in other languages likely have a different use, so it is important to not directly correlate how a class works in a language like Java to classes in JavaScript. There is not typical object-oriented inheritance, as the prototypical model remains in effect.

## Basic syntax

We already saw a quick example of a class, now let's define the various pieces of the syntax in more detail.

The primary way to define a class is to use a class declaration which has the `class` keyword followed by a name and `{}`. Inside, the only thing you can declare are methods. The special `constructor()` method runs when a new `Ledger` object is created to initialize some properties.

```js
class Ledger {
  constructor(balance) {
    this.balance = balance;
    this.transactions = [];
  }

  store(amount) { 
    this.transactions.push(amount);
  }

  clear() { 
    this.transactions = [];
  }
}

var myAccount = new Ledger(100); // New ledger starting with 100
myAccount.store(50); // I just saved 50!
myAccount.transactions; // Returns `[50]`;
```

To use a class, we must create an instance using the `new` keyword. The `constructor()` can take arguments, so anything passed in `new Ledger(100)` is made available to the `constructor()`.

All methods are declared without the use of the `function` keyword. The name you provide is made available so you can later call them like we did with `myAccount.store(50)`.

We've use the `this` keyword a few times to create or reference class properties. Any properties that are created are publicly available to access, as we did with `myAccount.transactions`.

> If you have worked with TypeScript you may have declared properties inside of a class as well. That is purely a TypeScript feature and not available in JavaScript directly.

It is unlikely you'll ever use the other way to define a class, called a class expression, so its not covered.

## A class as ES5

If we deconstruct our `Ledger` class, this is what it fundamentally looks like in ES5. When the class syntax is 'de-sugared', this will produce the same object.

```js
function Ledger(balance) {
  this.balance = balance;
  this.transactions = [];
}
Ledger.prototype.store = function(amount) {
  this.transactions.push(amount);
};
Ledger.prototype.clear = function() {
  this.transactions = [];
}
```

In the end, you get the same `Ledger` object.

## Constructor method

The constructor is a special method and is optional. However, it cannot be declared more than once. You only need one anyways, right?

Anything that you place inside of the `constructor()` method will run when a new instance is created. Therefore you should use it to do any initialization logic for your object, and can also accept arguments to setup internal state.

This is the best place to declare any properties that your object needs to retain. You can declare them inside of methods as well, but it is best to declare them in the constructor so you can be sure they are initialized before other methods might use them.

All properties stored on `this` are made public and can be directly accessed or modified.

## `this` and classes

The rules around what `this` refers to can be somewhat challenging, and classes are able to help ensure the context is more consistent.

Classes ensure that `this` always refers so the object instance, unless you add another block scope into a method. Essentially anytime you have a callback function, it will create a new scope and change the context of `this`. In this example, the `forEach` callback creates a new scope.

```js
class Ledger {
  constructor(transactions) {
    this.transactions = transactions;
    this.balance = 0;
  }

  calculateBalance () {
    // `this` refers to Ledger
    this.balance = 0;
    this.transactions.forEach(function forEachTransaction(transaction) {
    // `this` refers to forEachTransaction, oops
      this.balance += transaction;
    });
    return this.balance;
}
```

We can handle this using [arrow functions](arrow_functions.md), or other common methods like `function() {}.bind(this)`.

## Static methods

Static methods are used without instantiating a copy of the class, just like you do with the `Math.round()` or `Date.now()` methods. You declare a method to be static by using the \(you guessed it\) `static` keyword like so.

```js
class Circle {
  static circumference(radius) {
    return Math.PI * 2 * radius;
  }
}

var circumference = Circle.circumference(4); // 25.132741228718345
```

Static methods are called without instantiating the class first. In fact, static methods do not get attached to the prototype of the object, so they are not available when you create a new instance.

```js
var mycircle = new Circle(); // Create a class instance
mycircle.circumference(4); // undefined, not on prototype
```

This is important, because your static methods cannot access the rest of the object using `this`. Static methods should be standalone, and any inputs should be passed through as arguments.

If you want to call a static method inside of your class, you call it the same like `Circle.circumference(4)`. Since it is not bound to the prototype, other methods cannot access it either.

## Resources

* [Classes on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
* [You Don't Know JS - ES6 & Beyond - Classes](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20&%20beyond/ch3.md#classes)

