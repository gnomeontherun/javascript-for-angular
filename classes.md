# Classes

* [What are classes?](#what-are-classes)
* Syntax
  * Class Declaration
  * Class Expression
  * Hoisting
* Constructor method
* Prototype methods
* Understanding `this` and scope
* Static methods
* Subclassing
* Super classing
* Mixins
* Role of classes in Angular
  * Component and Directive Controllers
  * Services
  * Pipes
* Compared with ES5
* Best practices
* Things to avoid
* Resources

## What are classes?

Classes are a new way to define an object in JavaScript. They are only a new syntax to create objects, and do not directly introduce new concepts into the language itself. They are often referred to as **syntactic sugar** because it can make it easier to define and express objects.

When you use a class to create an object, it is fundamentally a function object. You would not use a class to define a new string or number object for instance.

You can define any number of properties and methods (technically just a property that happens to be a function) for a class. These properties can be set during object creation, using a constructor method to initialize the object, or can be modified after creation.

An object created with a class still uses prototypes. A new class will define a new prototype based on the properties and methods declared. Classes can extend another class, which will link the prototype of the class to the parent prototype. 

Classes in other languages likely have a different use, so it is important to not directly correlate how a class works in a language like Java to classes in JavaScript. There is not typical object-oriented inheritance, as the prototypical model remains in effect.

## Resources

* [Classes on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
* [You Don't Know JS - ES6 & Beyond - Classes](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20&%20beyond/ch3.md#classes)
