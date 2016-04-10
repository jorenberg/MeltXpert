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
