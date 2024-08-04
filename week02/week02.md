## HTML

HTML is a *declarative* language.

It focuses on *describing* the structure and content of a webpage without specifying *how* to achieve it.

### Features of HTML

- HTML contains *tags* (i.e. elements) that define the purpose or meaning of content
	
	`<p>This is a paragraph</p>`

- HTML elements contain attributes that provide additional information
	
	`<rect id="rectangle" x="2", y="3" />`

- HTML is a part of a suite of tools that encourage separation of concerns where each language has its own purpose:
	- HTML for structure
	- CSS for presentation
	- JavaScript for behavior

- HTML documents can be interpreted by web browsers

---

## TypeScript

TypeScript is a superset of JavaScript which supports type annotations.

```typescript
/*
Basic types: number, string, boolean, null, undefined, any
*/

let i: number = 123; // type annotation

// union types declare with '|' for variables that can take on multiple types
let x: number | string;
x = 2;
x = "Hello World!";

//function type annotations
function f(x: number, y: number): number {
	// ...
}

// higher order function type annotations
function curry(f: (x: number, y:number) => number)): (x: number) => (y: number) => number {
	return x => y => f(x, y)
}

// or using anonymous syntax
const curry: (f: ((x: number, y: number) => number)) => (x: number) => (y: number) => number
	= f => x => y => f(x, y)

// types
type OptionalNumber = number | null;

// types for object
type Todo = {
	timestamp: number;
	title: string;
	completed: boolean;
}

// generic type
type Thing<T> = {
	data: T;
}

// declaration
let numberThing: Thing<number> = {data: 2}

// recursive type
type BinaryTree<T> = Readonly<{ // read only object, immutable
  data: T;
  left?: BinaryTree<T>; // ? defines an optional property (can be null)
  right?: BinaryTree<T>;
}>;

// generic function
const curry: <T, U, V>(f: ((x: T, y: U) => V)) => (x: T) => (y: U) => V
	= f => x => y => f(x, y)


// checking types
typeof 1 // "number"
typeof "Hello World!" // "string"

// check null, Array
n === null // true
a instanceof Array // true




```

> Difference between `type` and `interface`
> 
> - Interfaces are open while types are closed, i.e. interface can be extended by declaring it again
> - Interface provide better error messages as the name of the interface will be used in the message
