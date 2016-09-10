# Default Parameter Values

* What are default parameters?
* Syntax
* Review

## What are default parameters?

In JavaScript, you can declare a function with any number of parameters. For example, a calculator function may accept two parameters, but only one is really considered required. You have to manually check if the value has been set, and if not provide a default value. 

So you may have written a snippet of code like the following.

```
function divide(a, b, precision) {
  if (Number.isNaN(a) || Number.isNaN(b)) {
    throw new Error('Must provide at least two numeric parameters to divide');
  }
  // Check if optional value was passed, and set a default
  if (Number.isNaN(precision)) {
    precision = 2;
  }
  // Divide with precision and parse as float
  return Number.parseFloat((a / b).toFixed(precision));
}
```

This works and ensures that `precision` is always set before being used in the final line, but we have to write the conditional check if the parameter is provided. 

However, with default parameters we can use a cleaner syntax to accomplish the same thing without having to write the additional conditional.

## Syntax

Default parameters are declared in the function declaration statement by adding `= 'value'` after the parameter name.

```
function sayHi(message = 'Hello World') {
  alert(message);
}

```

If we take the same example above we can rewrite it as follows.

```
function divide(a, b, precision = 2) {
 if (Number.isNaN(a) || Number.isNaN(b)) {
 throw new Error('Must provide at least two numeric parameters to divide');
 }
 // Divide with precision and parse as float
 return Number.parseFloat((a / b).toFixed(precision));
}
```

Any of the parameters in a function can be given a default value, they just have to be separated with a `,` like they do already.

```
function sendEmail(from = 'me@example.com', to = 'you@example.com') {
  // do email work
}
```

## Use cases

Default parameters are conceptually simple to understand and put into use, but here are a few 

## Review

