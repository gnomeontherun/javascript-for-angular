# Default Parameter Values

* What are default parameters?
* Syntax
* Review

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

If we take the same example above we can rewrite it as follows.

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

## Things to know

Before you put defaults into use everywhere, be aware of some of these common pitfalls and best practices.

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

## Review

