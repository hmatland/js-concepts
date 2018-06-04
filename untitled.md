# this – keyword

### What is the 'this' keyword used for?

`this` is perhaps the most misunderstood keyword in the language. Developers who are used to program in other languages, are most prone to misuse it. It is used as a reference variable, which its value depends on where it was used.

### Inside a function

When using strict mode, `this` will default to `undefined` unless it was specified by `.bind(thisValue)`. However, without strict mode, it will refer to the global object, `window` in browsers, and `global` in Node.

{% code-tabs %}
{% code-tabs-item title="Example 1" %}
```javascript
function someFunction() {
    // Browser
    console.log(this === window) // Output: true
    
    // Node
    console.log(this === global) // Output: true
}

function otherFunction() {
    'use strict'
    console.log(this) // Output: undefined
}

someFunction()
```
{% endcode-tabs-item %}
{% endcode-tabs %}



