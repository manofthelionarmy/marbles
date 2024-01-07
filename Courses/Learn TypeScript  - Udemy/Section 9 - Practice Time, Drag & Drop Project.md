[Links?](#)
[Decorator - Typescript Docs](https://www.typescriptlang.org/docs/handbook/decorators.html#decorators)
[Bind - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
[Decorator Pattern - Refactoring Guru](https://refactoring.guru/design-patterns/decorator)
[Embbed Videos?](#)
[Static Members - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/classes.html#static-members)
[static members - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static)
[Singleton - Design Patterns](https://refactoring.guru/design-patterns/singleton)
[Generics - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/generics.html#handbook-content)
[Abstract Classes and Members](https://www.typescriptlang.org/docs/handbook/2/classes.html#abstract-classes-and-members)
[Extends - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/extends)
[Super - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super)
[Getters/Setters - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/classes.html#getters--setters)
# Summary

----
# Related Stuff


----
# Notes:
- We create an object and used it to render our UI.
- We are registering event listeners to the form object via typescript.
	- We can use `bind` function or `decorators` to accomplish this.
- We create a `decorator` to bind our project input instance to the form-dom element when we add an event listener to it.
- Ex:
```typescript
// autobind decorator
function autobind(target: any, methodName: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value
  const adjDescriptor: PropertyDescriptor = {
    configurable: true,
    get() {
      const boundFn = originalMethod.bind(this)
      return boundFn
    }
  }
  return adjDescriptor
}

class ProjectInput {
// ...
  @autobind
  private submitHandler(event: Event) {
      event.preventDefault()
      console.log(this.titleInputElement.value)
  }

  private configure() {
    this.form.addEventListener('submit', this.submitHandler)
  }
// ...
}
```
- We had to configure `tsc` to use `decorators` because it is an experimental feature.
- I was tasked with creating my own way of increase reusability for the input validation functionality. The way I did it was use a variadic array of validate functions. Each of the functions I have return a function that matches the type alias:
```typescript
type ValidateInputFunc = (...s:string[])=>boolean

//...
class ProjectInput {
//...
  private validate(input: string[], ...validations:ValidateInputFunc[]): boolean {
    for (const f of validations) {
      if (!f(...input)) {
        return false
      }
    }
    return true
  }
//...
// ex:

private minLength(min:number): ValidateInputFunc {
    return (...elems:string[]): boolean => {
      for ( const s of elems ) {
        if (s.length < min) {
          return false
        }
      }
      return true
    }
  }

}
```
- The way Max (the instructor) implemented the input validation was via an interface. It appears interfaces don't mean the same as in golang, or other kinds of languages:
	- [Interfaces - Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#interfaces)
	- It looks like Max implemented the input validation in a different way, using the interface to configure how we want to validate our input.
### 2023-05-03:
- We are rendering the project list. To do that, we created a new class called `ProjectList`, and have member variables called `templateElement`, `hostElement`, and `section.` The block statements in the constructor consists of the same logic from `ProjectInput` class in order to render the template for our project lists. 
- There is some new syntax I have not seen:
```go
  private renderContent() {
    const listId = `${this.type}-project-lists`;
    // what's this syntax? this is new syntax to me
    this.section.querySelector('ul')!.id = listId;
    this.section.querySelector('h2')!.textContent = this.type.toUpperCase() + ' PROJECTS';
  }
``` 
### 2023-05-03:
- We created a class called `ProjectState` and used `static` and `private constructor`  to help create a `singleton` for state management. We also used the "`subscription`" model by invoking an array of call back functions in the event the state was changed (I don't like this, and is the singleton pattern even applicable).
### 2023-05-07:
- I did three videos today.
	- The first one was to create custom types Project, ProjectStatus, and Listener to replace class members or function parameters that were of type any.
	- The second video was to filter all projects and insert them in the correct list either by Active or Finished State.
	- In the third video, we did a large refactor by creating an abstract `Component` class and also used generics. We also used inheritance.
		- We refactored `ProjectInput` and `ProjectList` by converting them into sub-classes that implement the abstract `Component` class.
		- We also created a `State` class to utilize generics to. We then refactored `ProjectState` to be a subclass of State.
		- We also refactored `Listeners` and made it accept generics to. 
		- We had make `listeners` in `State` class be `protected` so that only sub classes can access `listeners` member variable and not publicly accessible outside of the class.
### 2023-05-11:
#### 09:28pm:
- I'm following along, we went over getters. 
## Questions:
- What is html `<template>` tag?
- Why did we have to do so much boilerplate to render our app?
- Why couldn't we not use `<template>`?
- How to make classes in Typescript?
- What is the `as` keyword? How is it related to type conversion?
- What does appending `!` to the end of an assignment do?
Ex:
```typescript
this.hostElement = document.getElementById('app')! as HTMLDivElement;
```
- What does `bind` do? Why do we need it?
	- In the case that we pass a private helper method as an event handler to an event listener, a local binding of `this` doesn't exist when it gets invoked. Recall an env in javascript refers to all of the bindings (global and local). When we invoke the event handler, which is a callback, there's no binding of `this` that exists in that context. Therefore, we have to bind `this` to the function via `bind`, which creates a local binding of `this` in that context.
Ex:
```typescript
private submitHandler(event: Event) {
  event.preventDefault()
	// when we bind, we now have have a local binding of this (I wonder what other stuff belongs to this...)
  console.log(this.titleInputElement.value)
}

private configure() {
// bind 'this' or reference to instatiation
	this.form.addEventListener('submit', this.submitHandler.bind(this))
}

```
- What type does `this` refer to if we don't use `bind`?
	- In the context of event handler function, this refers to the object which the event listener is bound to, which is the `form` object.
	 - without binding this, it will purely refer to form html element, not our instatiated object of type ProjectInput
	 - That means in this example:
```typescript
class A {
...
	cb() {
		console.log(this.message)	
	}
}
b.invokeCallBack(a.cb)
```
- When we have a function that accepts a call back, `this` refers to `b`. If we bind, then `this` also gets access to `a`'s  properties.
- When we bind, does the contents of the bounded `this` get copied over to the target `this`?
	- Yes :) 
- What is a decorator?
	- [Decorator - Typescript Docs](https://www.typescriptlang.org/docs/handbook/decorators.html#decorators)
 > A _Decorator_ is a special kind of declaration that can be attached to a [class declaration](https://www.typescriptlang.org/docs/handbook/decorators.html#class-decorators), [method](https://www.typescriptlang.org/docs/handbook/decorators.html#method-decorators), [accessor](https://www.typescriptlang.org/docs/handbook/decorators.html#accessor-decorators), [property](https://www.typescriptlang.org/docs/handbook/decorators.html#property-decorators), or [parameter](https://www.typescriptlang.org/docs/handbook/decorators.html#parameter-decorators). Decorators use the form `@expression`, where `expression` must evaluate to a function that will be <mark style="background: #FFB86CA6;">called at runtime</mark> with <mark style="background: #FFB86CA6;">information about the decorated declaration</mark>.
- Is the Decorator in Typescript inspired by the Decorators pattern in Design Patterns?
>  **Decorator** is a structural design pattern that <mark style="background: #FFB86CA6;">lets you attach new behaviors to objects</mark> by placing these objects inside <mark style="background: #FFB86CA6;">special wrapper</mark> objects that contain the behaviors.

 > “Wrapper” is the alternative nickname for the Decorator pattern that clearly expresses the main idea of the pattern. A _wrapper_ is an object that can be linked with some _target_ object. The wrapper contains the same set of methods as the target and delegates to it all requests it receives. However, <mark style="background: #FFB86CA6;">the wrapper may alter the result by doing something either before or after it passes the request to the target</mark>.
- Learn more about interfaces. They aren't the same as interfaces in golang. 
- What is this syntax?
```typescript
this.section.querySelector('ul')!.id = listId;
```
- What does `!` do?
- What does `?` do?
- What are generics?
- What does `abstract` do?
## Follow Up:
- Is the content copied over during a bind a deep or shallow copy?
