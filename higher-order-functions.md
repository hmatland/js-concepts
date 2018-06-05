---
description: >-
  Higher-order function is one of JS's great features which makes it great as a
  functional programming languages.
---

# Higher-order functions

### Definition

> A function that takes in a function as a parameter or returning a function are called **Higher-order functions**.

### When is it used?

We use it for callbacks, promises, functional iteration over arrays, array manipulation, etc. There are many applications for it.

###  Examples

{% code-tabs %}
{% code-tabs-item title="Example 1 – Array methods" %}
```javascript
let a = [1, 2, 3, 4,5]
let b = a.map(element => element * 2)

console.log(b) // Output: 2, 4, 6, 8, 10
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Example 2 – Array reduce" %}
```javascript
let a = [1, 2, 3, 4,5]
let b = a.reduce((memo, element) => memo += element)

console.log(b) // Output: 15
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Example 3 – Function as an argument" %}
```javascript
let strings = ['i', 'have', 'no', 'creativity', '🤔']

function logThis(message) {
    console.log(message + '\n')
}

function writeOut(stringArray, logger) {
    stringArray.forEach(logger)
}

writeOut(strings, logThis)

/* Output:
i

have

no

creativity

🤔
*/
```
{% endcode-tabs-item %}
{% endcode-tabs %}



