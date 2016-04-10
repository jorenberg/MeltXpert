# AMD [Asynchronous Module Definition]
The Asynchronous Module Definition (AMD) API specifies a mechanism for defining modules such that the module and its dependencies can be asynchronously loaded. This is particularly well suited for the browser environment where synchronous loading of modules incurs performance, usability, debugging, and cross-domain access problems.

## API Specification
### define() function
The specification defines a single function "define" that is available as a free variable or a global variable. The signature of the function:
```js
  define(id?, dependencies?, factory);
```

<a name="id" href="#id">#</a>&nbsp;<b>id</b>

The first argument, <b>id</b>, is a string literal. It specifies the <b>id</b> of the module being defined. This argument is optional, and if it is not present, the module <b>id</b> should default to the id of the module that the loader was requesting for the given response script. When present, the module <b>id</b> MUST be a "top-level" or absolute <b>id</b> (relative <b>ids</b> are not allowed).

<a name="moduleid" href="#moduleid">#</a>&nbsp;<b>module id format</b>

Module <b>ids</b> can be used to identify the module being defined, and they are also used in the dependency array argument. Module <b>ids</b> in AMD are a superset of what is allowed in CommonJS Module Identifiers. Quoting from that page:

- A module identifier is a String of "terms" delimited by forward slashes.
- A term must be a camelCase identifier, ".", or "..".
- Module identifiers may not have file-name extensions like ```".js"```.
- Module identifiers may be "relative" or "top-level". A module identifier is "relative" if the first term is "." or "..".
- Top-level identifiers are resolved off the conceptual module name space root.
- Relative identifiers are resolved relative to the identifier of the module in which ```"require"``` is written and called.

The CommonJS module id properties quoted above are normally used for JavaScript modules.

<b>Relative module ID resolution examples:</b>

- if module ```"a/b/c"``` asks for ```"../d"```, that resolves to ```"a/d"```
- if module ```"a/b/c"``` asks for ```"./e"```, that resolves to ```"a/b/e"```

If Loader-Plugins are supported in the AMD implementation, then "!" is used to separate the loader plugin's module <b>id</b> from the plugin's resource <b>id</b>. Since plugin resource <b>ids</b> can be extremely free-form, most characters should be allowed for plugin resource <b>ids</b>.

<a name="dependencies" href="#dependencies">#</a>&nbsp;<b>dependencies</b>

The second argument, ```dependencies```, is an array literal of the module <b>ids</b> that are dependencies required by the module that is being defined. The dependencies must be resolved prior to the execution of the module factory function, and the resolved values should be passed as arguments to the factory function with argument positions corresponding to indexes in the dependencies array.

The dependencies ids may be relative <b>ids</b>, and should be resolved relative to the module being defined. In other words, relative <b>ids</b> are resolved relative to the <b>module's id</b>, and not the path used to find the <b>module's id</b>.

This specification defines three special dependency names that have a distinct resolution. If the value of ```"require"```, ```"exports"```, or ```"module"``` appear in the dependency list, the argument should be resolved to the corresponding free variable as defined by the CommonJS modules specification.

The dependencies argument is optional. If omitted, it should default to <b>["require", "exports", "module"]</b>. However, if the factory function's arity (length property) is less than 3, then the loader may choose to only call the factory with the number of arguments corresponding to the function's arity or length.

<a name="factory" href="#factory">#</a>&nbsp;<b>factory</b>

The third argument, ```factory```, is a function that should be executed to instantiate the module or an object. If the factory is a function it should only be executed once. If the factory argument is an object, that object should be assigned as the exported value of the module.

If the factory function returns a value (an ```object```, ```function```, or any value that coerces to true), then that value should be assigned as the exported value for the module.

<a name="wrapping" href="#wrapping">#</a>&nbsp;<b>Simplified CommonJS wrapping</b>

If the dependencies argument is omitted, the module loader MAY choose to scan the factory function for dependencies in the form of require statements (literally in the form of ```require("module-id"))```. The first argument must literally be named require for this to work.

In some situations module loaders may choose not to scan for dependencies due to code size limitations or lack of toString support on functions (Opera Mobile is known to lack toString support for functions).

If the dependencies argument is present, the module loader SHOULD NOT scan for dependencies within the ```factory function```.

<a name="property" href="#property">#</a>&nbsp;<b>define.amd property</b>

To allow a clear indicator that a global define function (as needed for script "src" browser loading) conforms to the AMD API, any global define function SHOULD have a property called "amd" whose value is an object. This helps avoid conflict with any other existing JavaScript code that could have defined a ```define()``` function that does not conform to the AMD API.

The properties inside the define.amd object are not specified at this time. It can be used by implementers who want to inform of other capabilities beyond the basic API that the implementation supports.

Existence of the define.amd property with an object value indicates conformance with this API. If there is another version of the API, it will likely define another property, like define.amd2, to indicate implementations that conform to that version of the API.

An example of how it may be defined for an implementation that allows loading more than one version of a module in an environment:

```js
  define.amd = {
    multiversion: true
  };
```

The minimum definition:

```js
  define.amd = {};
```
