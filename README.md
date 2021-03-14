# JavaScript Variables
#
## Problem Statement

In this lesson, we'll introduce JavaScript variables and explain how to declare,
assign, and access them.

## Objectives

1. Define a variable
2. Name variables in JavaScript
3. Initialize variables in JavaScript
4. Identify when to use `const`, `let`, and `var` for declaring variables

## Define a Variable

A variable is a container in which we can store values for later retrieval.

Imagine a box that can hold any type of data: a number, string, true/false,
object — even an `undefined`. We take some data that we want to store, place it
inside the box, and hand the box off to JavaScript, which stores it in memory.
All done! Our data is safely stored until we need to access it again.

![Raiders of the Lost Ark warehouse](https://user-images.githubusercontent.com/17556281/28639657-fea1930a-7216-11e7-8c38-45bc9fab96a7.gif)

But wait! When we ask for the data back, how will JavaScript know _which_ box to
retrieve? We need to assign a name to our variable — a label for our box — so
that we can tell the engine exactly which piece of stored data we want.

## Name Variables in JavaScript

Variable names in JavaScript can sometimes be complicated, but if you follow
these three rules you'll be fine:

- Start every variable name with a lowercase letter. Variable names starting with a number are not valid.
- Don't use spaces — `camelCaseYourVariableNames` (see the camel humps?) instead of `snake_casing_them` (like the underscore is a snake that swallowed the words).
- Don't use JavaScript [reserved words][reserved words] or [future reserved words][future reserved words].

It's important to note that case matters, so `javaScript`, `javascript`,
`JavaScript`, and `JAVASCRIPT` are four different variables.

## Initialize Variables in JavaScript

The word `var` is a special word in JavaScript. It means that the word that
comes next is a _variable name_, an identifier for a box that we will put data
in. It was the _first_ way to declare a variable. For most JavaScript written
before 2015, only `var` is used for variables.

Now, let's use `var`.

```js
var pi;
//=> undefined
```

...and JavaScript sets aside a chunk of memory to store the declared variable.
Then, we assign a value to that variable:

```js
pi = 3.14159;
//=> 3.14159
```

We can package both of the initialization steps — declaration and assignment —
in a single line of code:

```js 
var pi = 3.14159; //=> undefined
```

Both of these methods are commonly used, so you could see and/or use either one.

To retrieve a declared variable, simply refer to its name:

```js
pi;
//=> 3.14159
```

### Variable Values

Upon declaration, all variables are automatically assigned the value of
`undefined`. It's only after we assign a new value that the variable will
contain something other than undefined. We can use `typeof` to check the data
type of the value currently stored in a variable:

```js
var language;
//=> undefined

typeof language;
//=> "undefined"

language = "JavaScript";
//=> "JavaScript"

typeof language;
//=> "string"
```

***Top Tip***: When writing JavaScript code, it's good practice to ***never*** set a
variable equal to `undefined`. Variables will be `undefined` until we explicitly
assign a value, so encountering an `undefined` variable is a strong signal that
the variable was declared before being used (or, as programmers say, being "referenced"). That's valuable information that we can use while debugging, and it comes at no
additional cost to us.

Once a variable has been created with `var`, we can reassign it to our heart's
content:

```js
var pi = 3.14159;
//=> undefined

typeof pi;
//=> "number"

pi = "the ratio between a circle's circumference and diameter";
//=> "the ratio between a circle's circumference and diameter"

typeof pi;
//=> "string"
```

The data that's stored in our variable might change over time, but at any moment we can retrieve its current contents:

```js
var language = "Mocha";
//=> undefined

language = "LiveScript";
//=> "LiveScript";

language = "JavaScript";
//=> "JavaScript";

language;
//=> "JavaScript";
```

## Identify When to Use `const`, `let`, and `var` for Declaring Variables

Because of its ubiquity in legacy code and StackOverflow posts, it's important
to get to know `var`. However, as we alluded to earlier, there is almost no
reason to use `var` with the features JavaScript has post-2015. `var` comes with
a ton of baggage in the form of scope issues (which we will discuss in the
lesson on scope in JavaScript) and allows developers to play a little too
fast and loose with variable declarations.

For example, with `var`, no error is thrown if you declare a variable twice:

```js
var language = "Ruby";
//=> undefined

var language = "JavaScript";
//=> undefined

language;
//=> "JavaScript"
```

This is bad! There's no reason to declare a variable twice, and it's usually a
mistake by a developer unaware that the variable had already been declared.

### `let`

ES2015 introduced two new ways to create variables: `let` and `const`. Both
solve all of `var`'s scope issues, which, again, we'll cover in the lesson on
scope in JavaScript. Both also throw an error if you try to declare the same
variable a second time:

```js
let pi = 3.14159;
//=> undefined

let pi = "the ratio between a circle's circumference and diameter";
//=> Uncaught SyntaxError: Identifier 'pi' has already been declared
```

Just like with `var`, we can still reassign a variable declared with `let`:

```js
let pi = 3.14159;
//=> undefined

pi = "the ratio between a circle's circumference and diameter";
//=> "the ratio between a circle's circumference and diameter"

typeof pi;
//=> "string"
```

### `const`

Using `let` instead of `var` will help you avoid silly errors like declaring the
same variable at two different places within your code, but there's an even
better option to use as your default: `const`.

Declaring a variable with the `const` reserved word means that not only can it
not be redeclared but it also ***cannot be reassigned***. This is a good thing
for three reasons:

1. When we assign a primitive value (any type of data _except_ an object) to a variable declared with `const`, we know that variable will _always_ contain the same value.
2. When we assign an object to a variable declared with `const`, we know that variable will _always_ point to the same object (though the object's properties can still be modified — more on this in the lesson about objects in JavaScript).
3. When another developer looks at our code and sees a `const` declaration, they immediately know that variable points to the same object or has the same value every other time it's referenced in the program. For variables declared with `let` or `var`, the developer cannot be so sure and will have to keep track of how those variables change throughout the program. The extra information provided by `const` is valuable, and it comes at no extra cost to you! Just use `const` as much as possible and reap the benefits.

```js
const pi = 3.14159;
//=> undefined

pi = 2.71828;
//=> Uncaught TypeError: Assignment to constant variable.
```

***NOTE***: With `let`, it's possible to declare a variable without assigning a value, just like `var`:

```js
let pi;
//=> undefined

pi = 3.14159;
//=> 3.14159
```

However, because `const` doesn't allow reassignment after the variable is initialized, we **must** assign a value right away:

```js
const pi;
//=> Uncaught SyntaxError: Missing initializer in const declaration

const pi = 3.14159;
//=> undefined
```

As your JavaScript powers increase with experience, you'll develop a more
nuanced understanding of what to use where. However, for now, this is a good
rule of thumb:

- ***Use `var`...*** never.
- ***Use `let`...*** when you know the value of a variable will change. For example, a `counter` variable that starts at `0` and is subsequently incremented to `1`, `2`, `3`, and so on. In the lessons on looping and iteration in JavaScript, `let` will have its moment in the spotlight.
- ***Use `const`...*** for _every_ other variable.

Best practice is to always declare variables with `const` and then, if you later
realize that the value has to change over the course of your program, circle
back to change it to `let`.

## Resources

- [MDN — Language basics crash course: Variables](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics#Variables)
- [Valid JavaScript variable names in ECMAScript 6][valid variable names]
- [MDN — `var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
- [MDN — `let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [MDN — `const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- [JavaScript ES6+: `var`, `let`, or `const`?](https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75)


[valid variable names]: https://mathiasbynens.be/notes/javascript-identifiers-es6
[reserved words]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Reserved_keywords_as_of_ECMAScript_2015
[future reserved words]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Future_reserved_keywords

## Conclusion

We covered what a variable is, how to initialize and retrieve it, and how to assign its values. We also looked at best practices for using `var`, `let` and `const`.
