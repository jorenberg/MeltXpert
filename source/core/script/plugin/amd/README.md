# AMD [Asynchronous Module Definition]
The Asynchronous Module Definition (AMD) API specifies a mechanism for defining modules such that the module and its dependencies can be asynchronously loaded. This is particularly well suited for the browser environment where synchronous loading of modules incurs performance, usability, debugging, and cross-domain access problems.

## API Specification
### define() function
The specification defines a single function "define" that is available as a free variable or a global variable. The signature of the function:
```js
  define(id?, dependencies?, factory);
```
