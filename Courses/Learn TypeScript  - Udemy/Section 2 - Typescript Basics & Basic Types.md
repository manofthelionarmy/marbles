[Links?](#)
[Static Type Checking - Type ScriptDocs](https://www.typescriptlang.org/docs/handbook/2/basic-types.html#static-type-checking)
[Types For Tooling - TypeScript Docs](https://www.typescriptlang.org/docs/handbook/2/basic-types.html#types-for-tooling)
[Non-exception Failures - TypeScript Docs](https://www.typescriptlang.org/docs/handbook/2/basic-types.html#types-for-tooling)
[Explicit Types - TypeScript Docs](https://www.typescriptlang.org/docs/handbook/2/basic-types.html#explicit-types)
[Type Annotations - TypeScript Docs](https://www.typescriptlang.org/docs/handbook/typescript-tooling-in-5-minutes.html#type-annotations)
[Structural Type System](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html#structural-type-system)
[Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#object-types)
[Embbed Videos?](#)
[Defining a Union Type - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#defining-a-union-type)
[Literal Types - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types)
[Type Aliases - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases)
# Summary

----
# Related Stuff

----
# Notes:
### Using Types:
- TypeScript adds typesafety.
- We can do a sanity check for any type violations by running tsc. 
- Tsc only helps us during development before we compile typescript into javascript.
- This won't affect the javascript at runtime because browsers don't have typescript support, browsers will run javascript. 
- So, what I learned from this is that we can throw silent errors when we run tsc (if and only if we configured tsc to do that) and not catch type check errors. This will still transpile the typescript into javascript, and the behavior didn't change. We did see the type coercion still happen in `"5" + 2.8 = "52.8"`. By doing type check errors and letting us catch it in development, we are able to minimize bugs caused by no type safety.
### TypeScript Types vs JavaScript Types
- I'll take a stab at what the basics are: at runtime when using javascript, we will find a type error or an error caused by an unhandled type being passed or used. We don't want to figure out at runtime, we want to catch type check errors during development, or during a compilation stage.
- Javascript has support for 3 types: 
	- strings
	- numbers
	- boolean
- Typescript has support for other types within its core types.
- The key difference is: Javascript uses "dynamic types" (resolved at runtime), TypeScript uses "static stypes" (set during development or compilation).
	- In other words, TS types are checked during compilation, JS types during runtime
- **The core primitive types in TypeScript are all lowercase!**
### Working With Numbers, Strings and Booleans
- What is it like working with numbers, strings, and booleans ?
	- It's the same, just make sure to do type declaration and assignment.
	- One thing I noticed in typescript is that it still won't say you from type coercion when you are peforming calculations (unless you assign to a type).
### Type Assignment and Type Inference
- Types can be inferred if we don't assign a variable to a type (or declare the type). Can be inferred with `let` and `const` keyword.
- The opposite of type inference is explicit typing (in code we assign a type)
- It is best practice to declare the type when we define a variable:
```typescript
let number1: number; // not inferred, or explicit assignment
const number2 = 2; // inferred assignment
const name: string = 'hello' // this is fine
let isRaining = true // this is fine
```
- `const` doesn't have to follow this, given it has to be bound to value when it is declared.
- Again, types allow you to detect errors early and avoid some runtime errors.
	- tsc will throw type check errors if assign the wrong value to a declared variable, even if it is inferred or not-inferred.
### Objects:
 - Typescript has syntax for an object type. 
 - One of the core types in typescript is `object`. If we use `object` as a type annotation, we won't get any information about properties.
 - In this lesson, we did an `anonymous object`, which is synatically creating an object type, but has no name:
```typescript
const person3: {
  name: string,
  age: number
} = {
  name: 'ralph',
  age: 30
}
```
### Array Types:
- Arrays have a type. 
- Traditional javascript array would be declared in typescript, but 
```typescript
let arr: any[];
```
- This defeats the point of typescript above. 
- [Arrays - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#arrays)
### Working With Tuples
- [Tuples - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#arrays)
> A _tuple type_ is another sort of `Array` type that <mark style="background: #FFB86CA6;">knows exactly how many elements it contains</mark>, and exactly which <mark style="background: #FFB86CA6;">types</mark> it contains at specific <mark style="background: #FFB86CA6;">positions</mark>.
- Example:
```typescript
const person: {
  name: string;
  age: number;
  hobbies: string[];
  role: [number,string]; // this special syntax tells typescript we have a tuple
} = {
  name: 'john',
  age: 49,
  hobbies: ['Sports', 'Cooking'],
  role: [2, 'author']
}

``` 
- If we were to do `person.role.push('admin'`, typescript won't pick up the error. The error we were expecting is that we went past the fixed length of the tuple after we used `push`.
- `person.role[0] = 'cook'` would cause typescript to throw an error; position 0 for this tuple should be a number.
### Enums
- [Enums - Typescript Docs](https://www.typescriptlang.org/docs/handbook/enums.html#handbook-content)
> Automatically enumerated global constant identifiers.
- Means they are translated to numbers
- This values also can start at a new initial value and increment by one (if all are numbers).
- We also get heterogeneous enums (meaning all the values can be different). 
### Any
- [Any - Typescript Docs ](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any)
- Really flexible
- Gives you the same experience with vanilla javascript.
> TypeScript also has a special type, `any`, that you can use whenever you don’t want a particular value to cause typechecking errors.
```typescript
let obj: any = { x: 0 };

// None of the following lines of code will throw compiler errors.

// Using `any` disables all further type checking, and it is assumed

// you know the environment better than TypeScript.

obj.foo();

obj();

obj.bar = 100;

obj = "hello";

const n: number = obj;
```
### Union  Types
- We can provide multiple type annotations to one type, especially for parameters in a function signature.
- We can check for the type at runtime. Or we don't have to all the time (idk what this means, and I need more examples).
```typescript
function combine(input1: number | string, input2: number | string) {
  let result;
  if ( typeof input1 === 'number' && typeof input2 === 'number' ) {
    result = input1 + input2
  } else {
    result = input1.toString() + input2.toString()
  }
  return result
}
```

> The first way to combine types you might see is a _union_ type. A union type is a type formed from two or more other types, representing values that may be <mark style="background: #FFB86CA6;">any one of those types</mark>. We refer to each of these types as the union’s _members_.
### Literal Types:
- Can use literal-types in unions
	- Meaning, the assigned value should be 1 of the values within the union (set).
```typescript
function combine(
  input1: number | string, 
  input2: number | string, 
  resultConversion: 'as-number' | 'as-text') {
  let result;
  if ( typeof input1 === 'number' && typeof input2 === 'number' 
    || resultConversion === 'as-number'
  ) {
    result = +input1 + +input2
  } else {
    result = input1.toString() + input2.toString()
  }
  return result.toString()
}
```

> But by _combining_ literals into unions, you can express a much more useful concept - for example, functions that only accept a certain set of known values.
### Type Aliases
>It’s common to want to use the same type more than once and refer to it by a single name.
>A _type alias_ is exactly that - a _name_ for any _type_.

> You can actually use a type alias to give a name to any type at all, not just an object type. For example, a type alias can name a union type

```typescript
type Combinable = number | string;
type ConversionDescriptor = 'as-number' | 'as-text';

function combine(
  input1: Combinable, 
  input2: Combinable, 
  resultConversion: ConversionDescriptor) {
  let result;
  if ( typeof input1 === 'number' && typeof input2 === 'number' 
    || resultConversion === 'as-number'
  ) {
    result = +input1 + +input2
  } else {
    result = input1.toString() + input2.toString()
  }
  return result.toString()
}

// type alias for object example
type Point = {  x: number;  y: number;}; 
```
> Note that aliases are _only_ aliases - <mark style="background: #FFB86CA6;">you cannot use type aliases to create different/distinct “versions” of the same type</mark>.
### Function Return Types and Void
- Functions can have return types. They can be explicitly stated via a type annotation applied in the function signature:
```typescript
function multiply(n1:number, n2:number): number {
  return n1 * n2
}
```
- Function return types can also be inferred.
- An observation I made is that functions that have an explicit return type makes the tsc compiler throw this error when the function is declared and is not invoked or returned value isn't read:
```
'multiply' is declared but its value is never read
```  
- Odd, I need to look in the docs why this is thrown. Maybe typescript has a rule where "if a funciton isn't used, remove it". It's weird it doesn't thrown that error if it's inferred. However, functions are first class citizens and are bindings themselves. It kinda makes sense we get that error if we declare a function with a return type and don't invoke it.
> `void` represents the return value of functions which don’t return a value. It’s the inferred type any time a function doesn’t have any `return` statements, or doesn’t return any explicit value from those return statements:
- Void means that a function returns no value. It's different from undefined.
```typescript
function print(num:number): void {
  console.log('Result: ' + num);
}
```
- [Void - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/functions.html#void)
- [Return Type Annotations](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#return-type-annotations)
- We don't have to use explicit return type annotations because the type can be inferred, however codebases may enforce this for documentation purposes (I can imagine, especially during a code review).
> Some codebases will explicitly specify a return type for documentation purposes, to prevent accidental changes, or just for personal preference.
### Functions As Types
- Functions are assignable. 
- If we declare a variable without a type annotation, by default it's implicit type is `any`.
- Therefore, this is legal and not good:
```typescript
function add(a:number, b:number) { return a + b}
let combineValues = add
combineValues = 5 // bad, defeats the puprose of typescript
```
- Thefore, we can give a variable a type annotation of a function type. The syntax for function types is similar to arrow functions. It can be anonymous function (I'm wondering if it can also be a type alias).
```typescript
type AddFunction = (a: number, b:number) => number;
let combinedValues: AddFunction;
...
let combinedValues: (a:number, b:number) => number;

```
- Oh neat, we can :) 
- [Function Type Expressions](https://www.typescriptlang.org/docs/handbook/2/functions.html#function-type-expressions)
### Function Types and Callbacks
- We can use function types for callback functions (functions we pass to be invoked).
- When we pass a call back as an arugment, typescript will check the type of the argument within the function type parameter against the parameter within the call back. It will be inferred if there's no type annotation, else tsc will complain that the function type's parameter doesn't match the type of the callback's parameter.
- This was an observation I made while coding and looking at the errors returned by tsc.
- Call backs can return something, even if function type argument on which they're passed does not expect a return type.
```typescript
// callback functions have to be function types
function addAndHandle(n1: number, n2:number, cb: (sum:number) => void) {
  let sum = n1 + n2 
  cb(sum)
}

addAndHandle(30, 20, (sum) => console.log(sum))

```
### The "unknown" type
- [Any, unknown, object, void, undefined, null, and never](https://www.typescriptlang.org/docs/handbook/type-compatibility.html#any-unknown-object-void-undefined-null-and-never-assignability)
> `any` and `unknown` are the same in terms of what is assignable to them, different in that `unknown` is not assignable to anything except `any`
- [unknown](https://www.typescriptlang.org/docs/handbook/2/functions.html#unknown)
> The `unknown` type represents _any_ value. This is similar to the `any` type, but is safer because it’s not legal to do anything with an `unknown` value.
- Kind of like interface in golang. We don't know what type we're dealing with, so we can check it or convert it to another type.
```typescript
function f1(a: any) {

a.b(); // OK

}

function f2(a: unknown) {

a.b(); // not ok, check the type, because we don't know if it's an object with function property b.

}
```
### never
- [never - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/functions.html#never)
> The `never` type represents values which are _never_ observed. In a return type, this means that the function throws an exception or terminates execution of the program.
- I noticed this when I tried to do something like this:
```typescript
function generateError(message: string, code: number): never {
  console.log(message, code)
}

const result = generateError('An error occured', 500)
console.log(result)
console.log('hello world')

``` 
- I got this error when trying to use that syntax:
 ![[Pasted image 20230417204135.png]] 
- By that definition, it looks like a throw statement makes this work.
- I wonder what other kind of javascript features makes code have an "unreachable point".
## Questions:
- Does heterogeneous enums defeat the purpose of typescript?
- Is there a way to configure the tsc compiler tool to not throw an error if we aren't "reading" the return type (which means invoking the function)?
	- I might have to configure a different linter for typescript then (typescript-eslint), there I can configure my linter.
	- odd, its not an error, but a warning for my regular nvim config and for lunar vim, it's configured to show an error. I have to see which linter null-ls uses for typescript. 
	- I think it's because typescript is configured to use eslint in ale (how, I don't have it installed)?
	- It may be using tsc by default 
	- I think I found it:
		- https://github.com/dense-analysis/ale/wiki/JavaScript-and-TypeScript-integration#tsserver-typescript
		- It uses tsserver as the default for linting in ale. Null-ls maybe using another linter by default. It's using tsc: https://github.com/jose-elias-alvarez/null-ls.nvim/blob/main/lua/null-ls/builtins/diagnostics/tsc.lua

## Follow Up:
- How to configure nvim and lunarvim to use typescript-eslint for linting?


