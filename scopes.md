# Scopes and closures

### Definition

> A scope essentially defines which variables you can use/access. A scope is divided into a **global**, and **local scopes**.

> A closure is an inner function, which has access to the parent/outer function scope.

### Scopes

Variables exposed in the global scope, will be accessible from within the global scope, and all the other underlying local scopes. However, a variable inside a local scope, will not be directly accessible from another local scope or from the global scope. When you are declaring a variable outside a function, then you are declaring a global variable.

#### Nested scopes

In Javascript, the child scope has access to it's parents variables. But not the other way around. This concept is named **lexical scoping**.

{% code-tabs %}
{% code-tabs-item title="Example 1" %}
```javascript
function someFunction() {
    /* Parent scope, relative to nestedFunction */
    let someVariable = 5
    
    function nestedFunction() {
        /* Child/nested scope */
        let nestedVariable = 0
        
        someVariable++ // This scope has access to someFunction's scope.
    }
    
    nestedVariable++ // This wont work! Parent scope does not have access to
                     // the nested/child scope.
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Block scopes

In ES6, a new way for declaring was introduced with `let` and `const`.  A local scopes is defined between curly braces. 

{% code-tabs %}
{% code-tabs-item title="Example 2" %}
```javascript
// This is the global scope
let someVariable = 0

function someFunction() {
    // Here is a local scope. We can access someVariable here.
    someVariable++
    
    if (/* some conditional */) {
        // Since let/const is block scoped. I can not access it outside
        // the curly braces it was declared in.
        let localScopedVar = 5
        
        // This works!
        someVariable++
    }
    
    // This won't work! This is outside the scope it was declared.
    localScopedVar++
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Scope chain

A scope chain, is a chain where the code needs to look for referenced variables. It starts searching in the local scope, and goes one scope up at a time if not found at that scope, until it reaches the global scope. It picks the first or "closest" assignment of that function or variable.

{% code-tabs %}
{% code-tabs-item title="Example 3" %}
```javascript
function someFunction() {
  let someString = 'Anduin Wrynn'

  function innerFunc() {
    return someString
  }

  return (() => {
    let someString = 'Something else'

    return innerFunc()
  })()
}

const res = someFunction()
console.log(res) // Output: Anduin Wrynn
```
{% endcode-tabs-item %}
{% endcode-tabs %}

In the example above, `someString` is defined twice. The declaration inside the anonymous function does not redeclare `someString` inside the `someFunction` scope. Since the redeclaration is in another function scope, it will not apply to `innerFunc` since it's scope chain is: `innerFunc scope` → `someFunction scope` → `global scope`. 

{% code-tabs %}
{% code-tabs-item title="Example 4" %}
```javascript
function someFunction() {

  let someString = 'Anduin Wrynn'

  function innerFunc() {
    return someString
  }

  return (() => {
    let someString = 'Something else'
    return someString
  })()
}

const res = someFunction()
console.log(res) // Output: Something else
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The scope chain for when searching for variable `someString` inside the anonymous function is: `anonymous func scope` → `someFunction scope` → `global scope`. 

#### Usage of global scope

The use of the global scope should be minimal. In the case of browsers, all of the code is sharing the same _namespace_. It means that, if you have a global variable for example in `index.js`,  then all other Javascript files will have access to the global variable. This can lead to collisions and more reserved variable names. But, due to the ES6 Modules, you can isolate each "module" or file, to have it own scope, and then instead export specific functions and variable from each module. If ES6 is not supported, you can use a **IIFE** – _Immediately invoked function expression_ _\(pronounced "iffy"\)_, which wraps the code inside a function scope, and then make use of global variables, outside that function scope. 

{% code-tabs %}
{% code-tabs-item title="Example 5" %}
```javascript
(function() {
    // Code    
})();
```
{% endcode-tabs-item %}
{% endcode-tabs %}

_It is recommended to use a semi-colon after an IIFE,_ due to that all included Javascript files are appended to each other in the browser. This side-effect of not using a semi-colon is that the IIFE is suddenly used as an argument for a function call, in the file before:

{% code-tabs %}
{% code-tabs-item title="Example 5 – No semicolon" %}
```javascript
// index.js
functionExpression = () => {
    console.log('I am not supposed to run.')
}
// someModule.js
(function() {
    // Code
})()
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This is a side-effect by **ASI** – _Automation semi-colon inserter_ in Javascript. After being processed by an uglifier/code-compressor, it might parse the IIFE as an function call to `functionExpression`. 

### Closures

A inner function has access to parent's scope, including function parameters. 

{% code-tabs %}
{% code-tabs-item title="Example 6" %}
```javascript
function someFunction() {
    const STATIC_STRING = 'Sylvanas Windrunner'
    
    return () => {
        // Has access to STATIC_STRING, inside this nested function.
        console.log(STATIC_STRING)
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}



