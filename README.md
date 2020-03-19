## JavaScript Style Guide
 1. [Comments](#Comments)
1. [Reserved Words](#Reserved-Words)
1. [Types](#Types)
1. [References](#References)
1. [Curly Braces](#Curly-Braces)
1. [Line Length](#Line-Length)
1. [Indents](#Indents)
1. [Semicolons](#Semicolons)
1. [Nesting Levels](#Nesting-Levelss)
1. [Function Placement](#Function-Placement)
1. [Style Guides](#Style-Guides)


### Comments

Comments -  are used to add hints, notes, suggestions, or warnings to JavaScript code. This can make it easier to read and understand. They can also be used to disable code to prevent it from being executed; this can be a valuable debugging tool.

There are two ways to add comments to code.

The first way is the ++//++ comment; this makes all text following it on the same line into a comment. For example:

    
``` js
function comment() {
    // This is a one line JavaScript comment
    console.log('Hello world!');
    }
    comment();
```

The second way is the ++/* */++ style, which is much more flexible.

For example, you can use it on a single line or make multiple-line comments:
```js
function comment() {
  /* This is a one line JavaScript comment */
  console.log('Hello world!');
}
comment();

function comment() {
  /* This comment spans multiple lines. Notice
     that we don't need to end the comment until we're done. */
  console.log('Hello world!');
}
comment();
```

### Reserved Words

In JavaScript you cannot use these reserved words as variables, labels, or function names:

+ abstract	
+ arguments	
+ await*	
+ boolean
+ break	
+ byte	
+ case	
+ catch
+ char	
+ class*	
+ const	
+ continue
+ debugger	
+ default	
+ delete	
+ do
+ double	
+ else	
+ enum*	
+ eval
+ export*	
+ extends*	
+ false	
+ final
+ finally	
+ float	
+ for	
+ function
+ goto	
+ if	
+ implements	
+ import*
+ in	
+ instanceof	
+ int
+ interface
+ let*	
+ long	
+ native	
+ new
+ null	
+ package	
+ private	
+ protected
+ public	
+ return	
+ short	
+ static
+ super*	
+ switch	
+ synchronized	
+ this
+ throw	
+ throws	
+ transient	
+ true
+ try	
+ typeof	
+ var	
+ void
+ volatile	
+ while	
+ with	
+ yield

++Words marked with * are new in ECMAScript 5 and 6.++

The following reserved words have been removed from the ECMAScript 5/6 standard:
+ abstract	
+ boolean	
+ byte	
+ char
+ double	
+ final	
+ float	goto
+ int	
+ long	
+ native	
+ short
+ synchronized	
+ throws	
+ transient	
+ volatile


### Types

#### Primitives: 
When you access a primitive type you work directly on its value.

+ string
+ number
+ boolean
+ null
+ undefined
+ symbol
+ bigint
```js
const foo = 1;
let bar = foo;

bar = 9;

console.log(foo, bar); // => 1, 9
```
Symbols and BigInts cannot be faithfully polyfilled, so they should not be used when targeting browsers/environments that don’t support them natively.

#### Complex: 
When you access a complex type you work on a reference to its value.

+ object
+ array
+ function
```js
const foo = [1, 2];
const bar = foo;

bar[0] = 9;

console.log(foo[0], bar[0]); // => 9, 9
```

### References

+ Use ++const++ for all of your references; avoid using var.
> ##### Why? This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.
```js
// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;
```
+ If you must reassign references, use ++let++ instead of var.

> ##### Why? let is block-scoped rather than function-scoped like var.
```js
// bad
var count = 1;
if (true) {
  count += 1;
}

// good, use the let.
let count = 1;
if (true) {
  count += 1;
}
```
+ Note that both ++let++ and ++const++ are block-scoped.
```js
// const and let only exist in the blocks they are defined in.
{
  let a = 1;
  const b = 1;
}
console.log(a); // ReferenceError
console.log(b); // ReferenceError
```
### Curly Braces

In most JavaScript projects curly braces are written in “Egyptian” style with the opening brace on the same line as the corresponding keyword – not on a new line. There should also be a space before the opening bracket, like this:
```js
if (condition) {
  // do this
  // ...and that
  // ...and that
}
```
A single-line construct, such as if (condition) doSomething(), is an important edge case. Should we use braces at all?

Here are the annotated variants so you can judge their readability for yourself:

:( Beginners sometimes do that. Bad! Curly braces are not needed:
```js
if (n < 0) {alert(`Power ${n} is not supported`);}
```
:( Split to a separate line without braces. Never do that, easy to make an error when adding new lines:
```js
if (n < 0)
  alert(`Power ${n} is not supported`);
```
;) One line without braces – acceptable, if it’s short:
```js
if (n < 0) alert(`Power ${n} is not supported`);
```
:) The best variant:
```js
if (n < 0) {
  alert(`Power ${n} is not supported`);
}
```
For a very brief code, one line is allowed, e.g. if (cond) return null. But a code block (the last variant) is usually more readable.


### Line Length
No one likes to read a long horizontal line of code. It’s best practice to split them.

For example:
```js
// backtick quotes ` allow to split the string into multiple lines
let str = `
  ECMA International's TC39 is a group of JavaScript developers,
  implementers, academics, and more, collaborating with the community
  to maintain and evolve the definition of JavaScript.
`;
```
And, for if statements:
```js
if (
  id === 123 &&
  moonPhase === 'Waning Gibbous' &&
  zodiacSign === 'Libra'
) {
  letTheSorceryBegin();
}
```
The maximum line length should be agreed upon at the team-level. It’s usually 80 or 120 characters.

### Indents

There are two types of indents:

Horizontal indents: 2 or 4 spaces.

A horizontal indentation is made using either 2 or 4 spaces or the horizontal tab symbol (key Tab). Which one to choose is an old holy war. Spaces are more common nowadays.

One advantage of spaces over tabs is that spaces allow more flexible configurations of indents than the tab symbol.

For instance, we can align the arguments with the opening bracket, like this:
```js
show(parameters,
     aligned, // 5 spaces padding at the left
     one,
     after,
     another
  ) {
  // ...
}
```
Vertical indents: empty lines for splitting code into logical blocks.

Even a single function can often be divided into logical blocks. In the example below, the initialization of variables, the main loop and returning the result are split vertically:
```js
function pow(x, n) {
  let result = 1;
  //              <--
  for (let i = 0; i < n; i++) {
    result *= x;
  }
  //              <--
  return result;
}
```
Insert an extra newline where it helps to make the code more readable. There should not be more than nine lines of code without a vertical indentation.

### Semicolons
A semicolon should be present after each statement, even if it could possibly be skipped.

There are languages where a semicolon is truly optional and it is rarely used. In JavaScript, though, there are cases where a line break is not interpreted as a semicolon, leaving the code vulnerable to errors. 

### Nesting Levels
Try to avoid nesting code too many levels deep.

For example, in the loop, it’s sometimes a good idea to use the continue directive to avoid extra nesting.

For example, instead of adding a nested ++if++ conditional like this:
```js
for (let i = 0; i < 10; i++) {
  if (cond) {
    ... // <- one more nesting level
  }
}
```
We can write:
```js
for (let i = 0; i < 10; i++) {
  if (!cond) continue;
  ...  // <- no extra nesting level
}
```
A similar thing can be done with if/else and return.

For example, two constructs below are identical.

#####
##### Option 1:
```js
function pow(x, n) {
  if (n < 0) {
    alert("Negative 'n' not supported");
  } else {
    let result = 1;

    for (let i = 0; i < n; i++) {
      result *= x;
    }

    return result;
  }
}
```
##### Option 2:
```js
function pow(x, n) {
  if (n < 0) {
    alert("Negative 'n' not supported");
    return;
  }

  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}
```
The second one is more readable because the “special case” of n < 0 is handled early on. Once the check is done we can move on to the “main” code flow without the need for additional nesting.


### Function Placement
If you are writing several “helper” functions and the code that uses them, there are three ways to organize the functions.

+ Declare the functions above the code that uses them:
```js
// function declarations
function createElement() {
  ...
}

function setHandler(elem) {
  ...
}

function walkAround() {
  ...
}

// the code which uses them
let elem = createElement();
setHandler(elem);
walkAround();
```
+ Code first, then functions
```js
// the code which uses the functions
let elem = createElement();
setHandler(elem);
walkAround();

// --- helper functions ---
function createElement() {
  ...
}

function setHandler(elem) {
  ...
}

function walkAround() {
  ...
}
```
+ Mixed: a function is declared where it’s first used.

Most of time, the second variant is preferred.
That’s because when reading code, we first want to know what it does. If the code goes first, then it becomes clear from the start. Then, maybe we won’t need to read the functions at all, especially if their names are descriptive of what they actually do.


### Style Guides
When all members of a team use the same style guide, the code looks uniform, regardless of which team member wrote it.

Some popular guides:
+ [Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml)
+ [Airbnb JavaScript Style Guide](http://dev.nodeca.com)
+ [Idiomatic.JS](https://github.com/rwaldron/idiomatic.js)
+ [StandardJS](https://standardjs.com/)