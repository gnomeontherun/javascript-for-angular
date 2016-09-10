# Arrow Functions

* What are arrow functions?
* Syntax
  * Fat arrows
  * Implied returns
  * Parentheses
  * 

* Always anonymous
* What about `this`?
* Things you can do with arrow functions
* Things you can't do with arrow functions

## What are arrow functions?

Arrow functions are a new syntax for creating function expressions that have a different set of rules governing their creation and use from standard functions. They are hailed for their shorter syntax, lexical `this`, and implied returns. Arrow functions have a basic syntax like this.

```js
(param[, param...]) => { statements; }
```

They are useful in a number of cases, but like classes they do not fundamentally change the way JavaScript itself works. A function is a function, regardless if it is an arrow function or standard function expression.

Let's take a quick example of a standard function expression. This is one of the most common types of examples for using arrow functions.

```js
var items = [1, 2, 3, 4, 5].map(function(n) {
  return n * n;
});
console.log(items); // [1, 4, 9, 16, 25];
```

We'll dig into the nuances of the use case shortly, but let here is the same function expression using arrow functions.

```javascript
var items = [1,2,3,4,5].map(n => n * n);
```

I think this simple example belittles the complexity of using arrow functions, but it does demonstrate the ability to write much more terse statements. Let's explore more of the syntax and underlying behaviors.

## Syntax



