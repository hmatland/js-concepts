# References

### Definition

If you're been working with C/C++ or other languages, you've then probably seen or used pointers to refer to memory addresses. In Javascript we use _references_. Of course, in Javascript we don't use pointers in the way that other languages do, but the concept is somewhat the same. However, there exist some limitations for references.

_Primitive types_ in JS are **passed by value**, which means that a variable is assigned to a another variable will not change the other, if one of them is changed.

However, _objects_ are **passed by reference**. This means that a variable does not "hold" the actual object, but rather a reference to that said object. When that variable with the reference is copied over to another variable, any change made to the object itself, will reflect on both. It's worth noting that since an _array_ is also an object,

### Examples

{% code-tabs %}
{% code-tabs-item title="Example 1" %}
```javascript
let xObj = {
    a: 1,
    b: 2
}

// Passed by reference, yObj copies the object reference that xObj holds.
let yObj = xObj

yObj.a = 42
xObj.a = 123

console.log(xObj) // Output: { a: 42, b: 123 }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

In the example you can see that they are editing the same object, although they are manipulated by two different variables. But there might be some confusion when there comes to reassigning. For example, when you're changing the variable `xObj` to another object, this change will **not** reflect on `yObj`. Why? Because when you're assigning an object to a variable, you only assign it's value. So when it comes to reassigning `xObj` , then you're only swapping out the old reference, but `yObj` still holds its reference to the old object. Here's an example.

{% code-tabs %}
{% code-tabs-item title="Example 2" %}
```javascript
let xObj = {
    a: 1,
    b: 2
}

// Passed by reference, yObj copies the object reference that xObj holds.
let yObj = xObj

// New object
xObj = {
    x: 123,
    y: 321
}

console.log(xObj) // Output: { x: 123, y: 321 }
console.log(yObj) // Output: { a: 1, b: 2 }
```
{% endcode-tabs-item %}
{% endcode-tabs %}



