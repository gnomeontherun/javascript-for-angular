# Default Parameter Values

* [What are default parameters?](#what-are-default-parameters)
* [Syntax](#syntax)
* [Things to know](#things-to-know)
  * [Defaults are evaluated at run time](#defaults-are-evaluated-at-run-time)
  * [No validation](#no-validation)
  * [Defaults can exist on any parameter](#defaults-can-exist-on-any-parameter)
  * [Triggering the default value](#triggering-the-default-value)

* [Review](#review)
* [Additional Resources](#additional-resources)

## What are default parameters?

In JavaScript, you can declare a function with any number of parameters. For example, a calculator function may accept two parameters, but only one is really considered required. You have to manually check if the value has been set, and if not provide a default value.

So you may have written a snippet of code like the following.

```
function divideNoDefaults(a, b, precision) {
  if (Number.isNaN(a) || Number.isNaN(b)) {
    throw new Error('Must provide at least two numeric parameters to divide');
  }
  // Check if optional value was passed, and set a default
  if (!Number.isInteger(precision)) {
    precision = 2;
  }
  // Divide with precision and parse as float
  return Number.parseFloat((a / b).toPrecision(precision));
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

If we take the first division example above, we can rewrite it as follows without the additional conditional statement to set the default value of `precision`.

```
function divideWithDefaults(a, b, precision = 2) {
 if (Number.isNaN(a) || Number.isNaN(b)) {
 throw new Error('Must provide at least two numeric parameters to divide');
 }
 // Divide with precision and parse as float
 return Number.parseFloat((a / b).toPrecision(precision));
}
```

Any of the parameters in a function can be given a default value, they just have to be separated with a `,` like they do already.

```
function sendEmail(from = 'me@example.com', to = 'you@example.com') {
  // do email work
}
```

Default values can also reference an external value. This can make writing code cleaner especially if there are multiple default values.

```
let from = 'me@example.com';
let to = 'you@example.com';
function sendEmail(from = from, to = to) {
  // do email work
}
```

## Things to know

Before you put defaults into use everywhere, be aware of some of these common pitfalls and best practices.

#### Defaults are evaluated at run time

The default value is always evaluated when the function is called, which means your default value may change over time. For example, maybe you want a default timestamp of the current time.

```
function logTime(now = Date.now()) {
  console.log(now);
}

logTime();
// Current timestamp will output
```

This can be a desired, but also a pitfall if you set a default value to an external value. If that external value changes, then the next time the function is called the default value will also be changed.

```
let loaded = new Date();
function logTime(now = loaded) {
  console.log(now);
}

logTime();
// Same timestamp will output
loaded = new Date();
logTime();
// New timestamp! Error?
```

#### No validation

Default parameters are unable to do any kind of validation that the value provided is a certain type. If you are assuming that a particular parameter is a particular type, you'll still need to validate it in your function.

Looking at our `divide` method earlier, there is a subtle difference in how the two versions will behave. The default parameter version removes the check to verify that the `precision` value is actually an integer.

```
divideNoDefaults(15, 2, 'three')
> 7.5

divideWithDefaults(15, 2, 'three')
> Uncaught RangeError: toPrecision() argument must be between 1 and 21(…)
```

Just because you have a default value doesn't mean an unacceptable value won't be passed, and you'll still want to validate input parameters before use.

#### Defaults can exist on any parameter

You can declare any parameter to have a default, regardless of the order. Some languages prevent this behavior, but not JavaScript. Take this example.

```
function divide(a = 1, b, precision = 2) {
  console.log(a, b, precision);
  // ...same function
}

divide(15, 3);
// 15, 3, 2
```

#### Triggering the default value

Since you can declare a default for any parameter, you might want to just accept the default value without having to declare it. If the first parameter has a default but not the second, you can force the default value by calling `undefined` as the first parameter.

```
function divide(a = 1, b, precision) {  
  console.log(a, b, precision);  
  // ...same function
}

divide(undefined, 3);
// 1, 3, undefined
```

This is essentially doing the same behavior as not providing a parameter at all, allowing the default to carry through. You can see here we removed the default value from `precision` and it will therefore be undefined.

#### Values can be any type

So far we've only showed simple values like a string or array. Default parameters can also be objects or arrays. For example, in this function it can accept an array of numbers to multiply together, but defaults to `[0]`.

```
function multiply(numbers = [0]) {
  let value = 1;
  numbers.forEach(function(num) {
    value *= num;
  });
  return value;
}

multiply();
// 0
multiply([4, 8, 12]);
// 384
```

Likewise, you can have an object with default property values.

```
function logEvent(config = { event: 'click', timestamp: Date.now() }) {
  console.log(config.event, config.timestamp);
}
```

## Review

Despite the length of this chapter, default parameters are conceptually simple. They essentially allow a more concise syntax for declaring a default value.

This leads to cleaner code, but doesn't inherently solve some other issues such as validation of parameter values.

## Additional Resources

* [MDN Default Parameters](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Default_parameters)
* [Clean Code with ES6 Default Parameters & Property Shorthands](https://www.sitepoint.com/es6-default-parameters/)

