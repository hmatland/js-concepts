---
description: >-
  All objects has properties and methods, in which are inherited from a
  prototype.
---

# Prototype and inheritance

### What is a prototype?

A prototype can somewhat remind of classes in other languages; inheritance, shared methods, etc. In Javascript, there are only a single primitive prototype; _object_. Every object has a prototype associated with it. You can create an object from another object, in which it inherits its properties and methods. 

### Inheriting a prototype

When you are prototyping, you can access the object itself by the `this` keyword \([read more about it here](untitled.md)\). 

{% code-tabs %}
{% code-tabs-item title="Example 1" %}
```javascript
let prototypeObj = {
    x: 5,
    g() {
        console.log(this.x)
    }
}

// Create a new object, which prototypes 'prototypeObj'
let newObj = Object.create(prototypeObj)

newObj.x = 10

// Inherits prototypeObj method
newObj.g()       // Outputs: 10
prototypeObj.g() // Outputs: 5
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Prototype chains

When an object is created from another object, it will _inherit_ it's prototype.

{% code-tabs %}
{% code-tabs-item title="Example 2" %}
```javascript
let x = {
  a: 1
}

let y = Object.create(x)
y.b = 2

let z = Object.create(y)
z.c = 3

// z object
console.log(z) // Output: {c: 3}

// y prototype
console.log(z.__proto__) // Output: {b: 2}

// z prototype
console.log(z.__proto__.__proto__) // Output: {a: 1}

// Object prototype
console.log(z.__proto__.__proto__.__proto__) // Object methods
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### The 'constructor' property

### When to use prototypes

[This StackOverflow answer sums it fairly good up.](https://stackoverflow.com/a/4737008)

