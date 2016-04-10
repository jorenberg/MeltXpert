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

<a name="multiple" href="#multiple">#</a>&nbsp;<b>Transporting more than one module at a time</b>

Multiple <b>define calls</b> can be made within a single script. The order of the define calls SHOULD NOT be significant. Earlier module definitions may specify dependencies that are defined later in the same script. It is the responsibility of the module loader to defer loading unresolved dependencies until the entire script is loaded to prevent unnecessary requests.

## Examples
### Using require and exports

Sets up the module with ID of "alpha", that uses ```require```, ```exports``` and the ```module``` with ID of "beta":

```js
   define("alpha", ["require", "exports", "beta"], function (require, exports, beta) {
       exports.verb = function() {
           return beta.verb();
           // Or:
           return require("beta").verb();
       }
   });
```

An <b>anonymous module</b> that returns an <b>object literal:</b>

```js
   define(["alpha"], function (alpha) {
       return {
         verb: function(){
           return alpha.verb() + 2;
         }
       };
   });
```

A <b>dependency-free module</b> can define a <b>direct object literal:</b>

```js
   define({
     add: function(x, y){
       return x + y;
     }
   });
```

A ```module``` defined using the simplified CommonJS wrapping:

```js
   define(function (require, exports, module) {
     var a = require('a'),
         b = require('b');

     exports.action = function () {};
   });
```

### Global Variables
This specification reserves the global variable <b>"define"</b> for use in implementing this specification, the package metadata asynchronous definition API and is reserved for other future CommonJS APIs. Module loaders SHOULD not add additional methods or properties to this function.

This specification reserves the global variable <b>"require"</b> for use by module loaders. Module loaders are free to use this global variable as they see fit. They may use the variable and add any properties or functions to it as desired for module loader specific functionality. They can also choose not to use <b>"require"</b> as well.

### Usage notes
It is recommended that define calls be in the literal form of ```'define(...)'``` in order to work properly with static analysis tools - like [build tools](http://gruntjs.com/).

### Relation to CommonJS
A version of this API started on the CommonJS wiki as a transport format, as Modules Transport/C, but it changed over time to also include a module definition API. Consensus was not reached on the CommonJS list about recommending this API as a module definition API. The API was transferred over to its own wiki and discussion group.

AMD can be used as a transport format for CommonJS modules as long as the CommonJS module does not use computed, synchronous ```require('')``` calls. CommonJS code that use computed synchronous ```require('')``` code can be converted to use the callback-style [require](https://github.com/amdjs/amdjs-api/wiki/require) supported in most AMD loaders.

<b>Note:</b> In MeltXpert®, We are using some loader plugins:

## 1. domReady
An AMD loader plugin for detecting DOM ready.

URL: https://github.com/requirejs/domReady

<b>Note:</b> Known to work in [RequireJS](https://github.com/requirejs/requirejs), but should work in other AMD loaders that support the same loader plugin API.

<a name="support" href="#support">#</a>&nbsp;<b>Page Load Event Support/DOM Ready</b>

It is possible when using RequireJS to load scripts quickly enough that they complete before the DOM is ready. Any work that tries to interact with the DOM should wait for the DOM to be ready. For modern browsers, this is done by waiting for the ```DOMContentLoaded``` event.

However, not all browsers in use support DOMContentLoaded. The domReady module implements a cross-browser method to determine when the DOM is ready.

<b>Usage:</b>

```js
  require(['domReady'], function (domReady) {
    domReady(function () {
      // This function is called once the DOM is ready.
      // It will be safe to query the DOM and manipulate
      // DOM nodes in this function.
    });
  });
```

Since DOM ready is a common application need, ideally the nested functions in the API above could be avoided. The domReady module also implements the Loader Plugin API, so you can use the loader plugin syntax (notice the <b>!</b> in the domReady dependency) to force the ```require()``` callback function to wait for the DOM to be ready before executing. domReady will return the current document when used as a loader plugin:

```js
  require(['domReady!'], function (doc) {
    // This function is called once the DOM is ready,
    // notice the value for 'domReady!' is the current document.
  });
```

<b>Note:</b> If the document takes a while to load (maybe it is a very large document, or has HTML script tags loading large JS files that block DOM completion until they are done), using domReady as a loader plugin may result in a RequireJS "timeout" error. If this a problem either increase the "waitSeconds" configuration, or just use domReady as a module and call ```domReady()``` inside the ```require()``` callback.

## 2. step
An AMD loader plugin for loaders like RequireJS that will load scripts in steps.

URL: https://github.com/requirejs/step

<b>Note:</b> This allows us to load traditional scripts that do not use AMD in a sequential fashion. You should prefer the built-in ```shim config``` in RequireJS to step, since it is more expressive and allows you to get local exports references. If you have a bunch of scripts with dependency sets that would make ```shim``` hard to use, then this plugin may help.

<a name="usage" href="#usage">#</a>&nbsp;<b>Usage:</b>

```step``` only works with AMD loaders that support [module config](http://requirejs.org/docs/api.html#config-moduleconfig), like RequireJS 2.0.

First, set up a module config for ```step``` and list out the steps in a ```steps``` property:

```js
 require.config({
  config: {
    step: {
      steps: [
          ['one'],
          ['two'],
          ['three'],
          ['four']
        ]
      }
    }
  });
```

In this example, four depends on three, two and one being loaded in order.

Then, to load a dependency along with anything in previous steps, use the ```step!``` loader prefix ID:

```js
  define(['step!four'], function () {
    // one.js, two.js and three.js will have also been
    // loaded by the time this function is called.

    // four.js creates a global `four` variable,
    // and it does not call define() so there
    // will not be a local `four` reference
    // passed to this function. Use the global `four` instead.
    console.log(four.doSomething());
  });
```

If you know that a script depends on two different scripts that each do not depend on each other, then you can put them in the same step. For instance, if "three" depended on "one" and "two" and "one" and "two" did not depend on each other:

```js
  require.config({
    config: {
      step: {
        steps: [
            ['one', 'two'],
            ['three'],
            ['four']
        ]
      }
    }
  });
```

<b>Note:</b> All the scripts in a step are loaded ```async``` and can load out of order, so it is
important that they do not depend on each other.

<a name="limitations" href="#limitations">#</a>&nbsp;<b>Limitations</b>

* Only use ```step``` with scripts that do not already call ```define()```. Similarly, do not include scripts in ```step``` that depend on AMD modules.
* It is slower loading than loading plain AMD modules. ```step``` waits for each previous step to complete loading before doing the next step. Doing an [r.js optimization build](http://requirejs.org/docs/optimization.html) when you are ready to deploy your code is strongly suggested.
* When doing a build, include all the steps in the build output. If you use an `exclude` directive to exclude a step script, it will likely break when that built file is run in the browser.
* ```step``` will read the step config the first time it is called, and "burn in" that config internally. So, it will not understand any further step config if it is set after the first ```step!``` reference.
