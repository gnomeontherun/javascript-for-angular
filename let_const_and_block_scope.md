# Let, Const, and Block Scope

* [Why we needed more variable keywords](#why-we-needed-more-variable-keywords)
* [Syntax](#syntax)
* [Things to know](#things-to-know)
* [Review](#review)
* [Additional Resources](#additional-resources)


## Why we needed more variable keywords

Many pixels have been spent covering the issues with using `var` in JavaScript. Many of these concerns have been mitigated by the use of `strict mode` and several coding techniques. 

So while many JavaScript developers have been able to use tricks like IIFE to encapsulate variables, these are always hacky and cumbersome. Fundamentally, the problem lies in the scoping of variables declared with `var` and how it is possible to write code that references variables from an unsuspecting scope.

Block scope has always existed in JavaScript, but variables declared with `var` do not know about block scope. Declaring a block scope occurs anytime you see a set of curly braces `{}`, usually in connection with flow control statements (like `if` or `for`). To illustate this problem, we can create a block scope that causes a logic collision with some variables.

```
var day = 'Monday';
if (true) {
  var day = 'Tuesday';
}
console.log(day); // Tuesday
```

Since variables declared with `var` don't look at block scope, we are actually redeclaring the `day` variable. This may be a trival code example, but name collisions are harder to avoid in a larger codebase.

You likely know about this issue, but we can now create variables using `let` or `const` that are scoped to the block they are declared.

## Syntax

Using `let` and `const` is simple, you just put it in front of a variable name just like you do with `var`.

```
let myState = 'Texas';
const myName = 'Jeremy';
```

Using the `let` keyword, we can declare a variable that is limited to the current block scope and fix our issue from earlier. 

```
var day = 'Monday';
if (true) {
  let day = 'Tuesday';
}
console.log(day); // Monday
```

This means that variable names from different block scopes will no longer collide. 


## Things to know

#### Cannot redeclare same variable name

If you have already declared a variable by a given name in a block, you cannot redeclare it.

```
function getMap() {
  let state = 'texas';
  // ...other code
  let state = 'montana'; // SyntaxError
}
```

#### Cannot reassign `const`

This is a tricky

#### `const` only applies to variable, not value

The restrictions of `const` do not carry through when you assign it to another value. That variable remains a pointer 

```
const prop = 1;
const item = {
 prop: prop
};
item.prop = 2;
console.log(item);
```

## Review



## Additional Resources

* [MDN Let](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Default_parameters)

