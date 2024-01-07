[Links?](#)
[Embbed Videos?](#)
[Strict Mode - Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)
[Bind Event Handlers in Web Components](https://www.freecodecamp.org/news/this-is-why-we-need-to-bind-event-handlers-in-class-components-in-react-f7ea1a6f93eb/)
# Summary
- In assignment statements, if there is no implicit binding, we will fall back to a default binding.
- In a assignment statement to an object's prototype function, because there is no implicit binding to infer that `this` refers to the instantiated object, `this` defaults to `globalThis`
- Because classes execute in strict mode, assignment statements involving class methods result in the default binding returning `undefined`.
- When we assign class methods to event handlers, i.e. `onclick`, this "phenomena" happens, hence why we bind this to class methods. This is called an explicit binding via `Object.prototype.bind()`.

----
# Related Stuff
[[Web components]]
[[Lit Web Components]]
[[Lit Web Components Playground]]
#javascript 
#webapplications 

----
# Notes:
- It seems a little weird, but this code explains why we bind in the constructor:
```javascript
class Foo {
  constructor(name){
    this.name = name
  }
  
  display(){
    console.log(this.name);
  }
}

var foo = new Foo('Saurabh');
foo.display(); // Saurabh

// The assignment operation below simulates loss of context 
// similar to passing the handler as a callback in the actual 
// React Component
var display = foo.display; 
display(); // TypeError: this is undefined
```
- The implicit binding when we invoke the function in `foo.display()` is that `this` is the instance `foo`.
- However, the binding vanishes when we do an assignment statement. The `this` defaults to the next closest scope, and in this context, it is the global scope.
- That is why we use `bind()`; to ensure in the assignment statement that the object falls back to the actual bound instance, which is the instantiated class object, i.e. `this`. 
> In this case, the value of this inside display() <mark style="background: #FFB86CA6;">falls back to default binding</mark>. It points to the global object or undefined if the function being invoked uses strict mode.
- So when we invoke the function preceded by the object, i.e. obj.outerDisplay(), there is an implicit binding.
- After an assignment statement to a class method and then we invoke the function, because there is no implicit binding (or preceding object to method invocation), it falls back to the default binding.
- In the context of assigning to a class method, `this` is undefined. Why isn't is the global `this`?
- What happened is <mark style="background: #FFB86CA6;">the this value was undefined as the context was lost after passing the handler as a callback</mark> — synonymous with an assignment operation.
- The <mark style="background: #FFB86CA6;">bodies of class declarations and class expressions are executed in strict mode</mark>, that is the constructor, static and prototype methods. Getter and setter functions are executed in strict mode.
- There's this rule when executing in strict mode:
> <mark style="background: #FFB86CA6;">The value passed as this to a function in strict mode is not forced into being an object</mark> (a.k.a. "boxed"). For a sloppy mode function, this is always an object: either the provided object, if called with an object-valued this; or the boxed value of this, if called with a primitive as this; or the global object, if called with undefined or null as this. (Use call, apply, or bind to specify a particular this.) Not only is automatic boxing a performance cost, but <mark style="background: #FFB86CA6;">exposing the global object in browsers is a security hazard</mark> because the global object provides access to functionality that "secure" JavaScript environments must restrict. Thus <mark style="background: #FFB86CA6;">for a strict mode function, the specified this is not boxed into an object</mark>, and if unspecified, this is <mark style="background: #FFB86CA6;">undefined instead of globalThis</mark>:

- So, normally in an assignment statement to a class method, the binding/variable will fall back to the default binding, which is `globalThis`
- Since classes are in `strict mode` by default, the assignment won't result in `globalThis`, it would result in `undefined` according to the strict rule.
## Questions:

## Follow Up:
