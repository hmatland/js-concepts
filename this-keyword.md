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

### Inside an object

Inside a object, `this` will reference to the object itself, but not it's not how you might think! The following example will **not work**:

{% code-tabs %}
{% code-tabs-item title="Example 2" %}
```javascript
let x = {
    a: 42,
    b: this.a
}

console.log(x) // Output: { a: 42, b: undefined }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Why is this so? When you're trying to refer to `this` ,  it will fail, due to that the object is not defined yet. However, you could wrap it around a function. **TODO: write about arrow vs normal function**

