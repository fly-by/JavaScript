# Javascript

JavaScript is a mixture of object-oriented programming (objects, inheritance) and functional programming (higher-order functions: built-in  map, reduce, etc.).

# About _fly-by_
The objective of the technology _fly-by_ series is to just touch every significant feature briefly but always provide the technical terms. It should make you more firm in talking about the respective technology but not so much introduce you to it.

## Setup

### JS in bash scripts

#### Install NodeJS
```bash
sudo apt-add-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
sudo apt-get install npm  # You probably want this too, for development purposes
```

#### Interpreter directive in bash scripts
```js
#!/usr/bin/env node

// array: filename, absolute path, arguments
global.process.argv

// include another JS file
require('./relativePath.js')
```

More in the [NodeJS documentation](http://nodejs.org/api/).

***

## Concepts

### Strict mode
***Strict mode*** enables more warnings. The non-strict default mode is called ***sloppy mode***. It can be enabled function- or file-wise using `'use strict';`.

### Compilation Phases
1. ***Tokenizing/Lexing***
Breaking down the sourcecode into parsable chunks.
2. ***Parsing***
Turning the stream of tokens into an ***AST (abstract syntax tree)***
3. ***Code-Generation***
Turning the AST into machine executable code.

### Statements/Expressions
***Statements*** "do things"/have ***(side) effects*** (eg. `var a` has the effect of introducing a new variable) but do not return values whereas ***expressions*** produce and return values and thus can be used whereever a value is expected (eg. `2*3`). A single line like `func(3)` that combines both aspects is called a ***expression statement***. Statements can be ended explicitly with a semicolon or implicitly with a linebreak relying on ***automatic semicolon insertion***.

TODO: This is unsatisfying! Arbitrary distinction?! What does the language standard say?

### Automatic Semicolon Insertion (ASI)
ASI virtually inserts a semicolon at the end of a line except:

1. The statement is unfinished.
2. Another statement or block is reqiured.
3. The next line starts with `[`,  `(` or an operator.

### Scope
***Scope*** means the area of accessability of variables and functions. Eg. a function can be defined in/attached to a scope in which it can access a certain variable or not.

JS utilized ***function based*** ***nested*** ***lexical*** scope which allows for ***shadowing***.

#### Function based scope
Only functions bodys not blocks (areas between curly braces) or other constructs introduce scope.

#### Nested scope
Functions can be declared within functions. Every new function has access to its surrounding scope but not to other functions scope that are declared adjacent to it. The surrounding scope is called the ***outer scope*** of that function the scope within it the ***inner scope***. Variables and functions defined directly within in the inner scope are called ***local***. Defined directly in the very first scope/the outermost scope/the ***global scope*** they are called ***global***.

#### Lexical scope
Lexical scope means that each function stays connected to the variables that surrounded it at the point in code where it was defined regardless from where it is called. We say functions ***close over*** their environment. If we speak of a function with respect to its connected environment we call it a ***closure***.

#### Shadowing
Shadowing takes place when a variable or function name is used for a declaration eventhough it already holds a value or function in the current scope. Then that name is "overwritten" in the inner scope and all additional scopes that may be nested there. We say eg. "the variable a is shadowed by the ***local variable*** b".

### Hoisting
Function and variable declarations (but not function expressions and not assignments) are ***hoisted*** meaning they are virtually moved to the beginning of the scope in which they live so they can be called before their definition.

### Values
JS knows six ***value types***:

1. `undefined` (meaning: "no value"/"nonexistence")
2. `null` (meaning: "no object"/"emptyness")
3. Booleans
4. Strings
5. Numbers
6. Objects

`null` and `undefined` are also called ***nonvalues***.
 
Every value has an Unicode ***identifier*** (a name so to speak) and ***properties***. Only on objects can properties be changed or added. I guess because of that are all values except objects called ***primitve values*** or short ***primitives***.

#### Properties
Each property has a Unicode ***key***/***name*** and a value. `null` and `undefined` are the only values for which any property access results in an exception instead of `undefined`.

#### Right hand side lookup (RHS)
The retrieval of the value of a variable starting in the current scope working the nested scope chain upward to the outermost/global scope. Failure raises a `ReferenceError`.

#### Left hand side lookup (LHS)
The search for the storage space/the container of a variable (and the scope to which it is associated) when a value is assigned to it. Failure in sloppy mode creates a new variable in the global scope. Failure in strict mode raises a `ReferenceError`.
