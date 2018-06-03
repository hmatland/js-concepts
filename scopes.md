# Scopes and closures

### Definition

> A scope essentially defines which variables you can use/access. A scope is divided into a **global**, and **local scopes**.

### Scopes

Variables exposed in the global scope, will be accessible from within the global scope, and all the other underlying local scopes. However, a variable inside a local scope, will not be directly accessible from another local scope or from the global scope. When you are declaring a variable outside a function, then you are declaring a global variable.

#### Block scopes

In ES6, a new way for declaring was introduced with `let` and `const`.  A local scopes is defined between curly braces. 

{% code-tabs %}
{% code-tabs-item title="Example 1" %}
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



