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

There are also features of JS that allow for functional programming to happen.

1. Anonymous functions: functions that do not need to be defined with a name
2. Functions as objects: variables can contain functions
3.  Higher - order functions - functions can be passed into other functions as arguments + functions can be returned by other functions

```javascript
const anon1 = () => "Hello World!"

const anon2 = function() {
	return "Hello World!"
}

function higherOrder1() {
	return (name) => "Hello, " + name
}

function higherOrder2(f, number) {
	return f(number)
}
```

The methods of the `Array` class in JavaScript are also higher-order functions that make manipulating elements in an array easy.

`map`, `filter` and `reduce` are particularly useful.

```javascript
let arr = [1, 2, 3]

arr.map((x) => x * 2) // [2, 4, 6]
arr.filter(x => x % 2 !== 0) // [1, 3]
arr.reduce((ac, x) => ac + x, 0) // 6
```

---
## Introduction to Functional Programming

### Side Effects, Purity, Referential Transparency

A *side effect* of a function is when the function changes some state outside of its scope.
- changing a value outside the function scope
- printing to output
- etc

A function is considered *pure* if it:
- has no side effects
- always produces the same result for some input

In the context of FP, we do not think of a variable as a 'container' that stores a value, rather just an alias for the value. Following this, *all variables in functional programming are immutable*.

There is also *referential transparency*, which means that we can *substitute an expression that evaluates to some value, with that value, without affecting the output of the program*. Usually, this means that we can substitute the function for its output, in functional programming.

For example, an impure function:

```javascript
let global_counter = 0

const impureFunc = () => {
	global_counter++
}
```

Demonstrating referential transparency:

```javascript
const square = (x) => x*x

square(square(2))
// it is possible to substitute square(2) since it is pure
square(4)
8
```

---
## Cons List

We can model a linked list only using functions to capture data.

The following parts require prior understanding on anonymous functions.

```javascript
(x) => x + 1 // anonymous function

// calling an anonymous function with a parameter
((x) => x + 1)(2) // 3
```

---

Consider the function below.

```javascript
function cons(head, rest = null) {
	return (selector) => selector(head, rest)
}
```

The above function `cons` returns an anonymous function, `(selector) => selector(head, rest)`
which takes in a function `selector` as parameter and calls `selector` with the parameters `head` and `rest`.

`head` refers to the current node in the linked list, and `rest` refers to the rest of the linked list.

We can define a cons list as follows:

```javascript
let list = cons(1, cons(2, cons(3, null)))
```

 Note that it is equivalent to the following chain of anonymous functions (by expanding `cons`):

```javascript
let list = (s1) => s1(1, (s2) => s2(2, (s3) => s3(3, null)))
```

We now define two `selector` functions for our linked list, to obtain either the `head` or the `rest` of the linked list:

```javascript
function s_head(list) {
	return list((head, _) => head)
}

function s_rest(list) {
	return list((_, rest) => rest)
}
```

It is now possible to access certain elements from our linked list:

```javascript
let list = cons(1, null)

// we will simplify the above to see how the head is obtained
s_head(list) // 1

// ---- the above is equivalent to all the below ----
list((head, _) => head)
cons(1, null)((head, _) => head)

// we can see that we are calling the anonymous function with the head selector, (head, _) => head
((s1) => s1(1, null))((head, _) => head)

// we continue simplifying...
((head, _) => head) => s1(1, null)
((head, _) => head))(1, null)

1 // head
```

The above code looks really confusing, so we will try to simplify it by substituting all anonymous functions with named functions instead:

```javascript
// we omit the cons because it is not that relevant in this case

function cons(head, rest) {

	function run_selector(selector) {
		return selector(head, rest)
	}

	return run_selector
}

let list = cons(1, null)

// equivalent to s_head
function s_head(list) {

	// equivalent to (head, _) => head
	function get_head(head, rest) {
		return head
	}

	return list(get_head)
}

s_head(list)

// ---- the above is equivalent to all the below, we continue simplifying ----
list(get_head)
run_selector(get_head)
get_head(1, null)
1 // head
```

From the above, it is understood that the process of trying to get the `head` / `rest` of a cons list is as follows:

1. We call `head` / `rest` on our cons list
2. our cons list calls a selector function to extract the `head` / `rest`
3.  the selector function runs with the two arguments from the cons list and returns `head` or `rest` respectively.

