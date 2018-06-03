# Scopes and closures

### Definition

> A scope essentially defines which variables you can use/access. A scope is divided into a **global**, and **local scopes**.

### Scopes

Variables exposed in the global scope, will be accessible from within the global scope, and all the other underlying local scopes. However, a variable inside a local scope, will not be directly accessible from another local scope or from the global scope. When you are declaring a variable outside a function, then you are declaring a global variable.

#### Nested scopes

In Javascript, the child scope has access to it's parents variables. But not the other way around. This concept is called **lexical scoping**.

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

### Closures



