# Week 01

## Syntax vs Semantics

Syntax - The *set of symbols and rules* that define a programming language.

Semantics - The *meaning* of the symbols and rules, i.e. syntax that allows a computer to perform specified tasks.

Two pieces of code can have different syntax, but the same semantics (i.e. trying to achieve the same outcome). For example:

```python
def sumTo(n):
    sum = 0
    for i in range(n):
        sum += i
    return sum
```

```c
int sumTo(int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
    {
        sum += i;
    }
    return (sum);
}
```

The two functions do the same thing (same semantics) in different programming languages (different syntax).

## Programming Paradigms

A programming paradigm is a certain style of programming with its own syntax and semantics.

Paradigms are created to abstract away uneccessary complexity when programming a computer (for example, machine code, assembly), and as such there are many different paradigms.

### Hirearchy of Programming Paradigms

![paradigms](/assets/paradigms.png)

Programming paradigms can be divided into two main groups.

1. Imperative programming - Define a sequence of statements that changes a program's state

    - Procedural: Has the concept of procedures (a.k.a. functions) that may be invoked elsewhere in the program.  
    - Object - Oriented: Has the concept of objects which captures data (i.e. state) and behaviors (i.e. methods) associated with entities in a system.

2. Declarative programming - Define what a procedure should do rather than how it should do it

    - Functional: Has the concept of composable functions (i.e. functions can be made up of other functions, taken in as arguments to other functions, or return new functions), which is based on lambda calculus.
    - Logical: Programs are defined as logical statements

Currently, many programming languages are also multi-paradigm in the sense that they provide support different paradigms.

## JavaScript

JavaScript is a multi-paradigm language which just so happens to support higher-order functions, a core concept of Functional Programming.

```javascript
let x = 5 // mutabale variable, can be reassigned
const y = 10 // immutable variable, cannot be reassigned

x = 'a' // no error. also, dynamic typing
y = 20 // error

// scope
{
    let secret = 2
}
console.log(secret) // error

if (x === 1 || y !== 10) // strict equality, '==' for loose equality
    console.log("X is one") // print using console.log

// shorthand if statement (ternary operator '?')
// condition ? return value if true : return value if false
let z = (x === 1 || y !== 10) ? x : y

// while loop
while (x < 5)
{
    x += 1
}

// for loop
for (let i = 0; i < y; i++)
{
    console.log(i)
}

// named function
function foo() {
    return "Hello World!"
}

// anonymous function 1: a.k.a. arrow function
const foo_anon1 = () => "Hello World!" // no braces will return value

// anonymous function 2
const foo_anon2 = function() {
    return "Hello World!"
}

// NOTE: recursion exists in functions

// array
let a = [1, 2, 3]

let b = [4, ...a] // spread operator unpacks the iterator

// object
let obj = {
    attribute: 1, // attributes
    attribute2: 2
}

// access attributes
console.log(obj.attribute)
console.log(obj['attribute2'])
```

balls

## Functional Programming in JavaScript

oh boy
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNzc3MDMxMF19
-->