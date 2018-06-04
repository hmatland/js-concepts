# Promises

### Definition

A promise, put in simple terms, is a set of callbacks that are called when an operation is done. This is incredibly useful for when using dealing with REST APIs, or other async code.  

### Making a promise

To make a promise is fairy simple:

{% code-tabs %}
{% code-tabs-item title="Example 1" %}
```javascript
function someFunction() {
    return new Promise((resolve, reject) => {
        let data = []
        
        // Some async operations
        
        if (someError) {
            // If there is an error.
            reject('Some error message')
        } else {
            // Operation was successful, return data.
            resolve(data)
        }
    })
}

// Then we can do this:
someFunction().then(resolvedData => {
    // Handle data that was resolved.
    console.log(resolvedData)
}).catch(errorMessage => {
    // Handle when there is a error
    console.log(errorMessage)
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}

You create a new promise at line 2. Here pass an anonymous function with two parameters: `resolve`, and `reject`.  These are callback functions for whether your promise "fails" or not. To return some data or "fulfill the promise" is done by calling `resolve`. At line 18, the function is called, and instantly returning a promise object. `.then` is a method of the promise object. Here you supply a callback function, in which is invoked when the promise calls `resolve`. `.catch` is used for error-handling, and is invoked when `reject` is called. It supplies the same parameters 

### Waiting for multiple promises

If there is a case when you need to wait before all promises are fulfilled, then you can use `Promise.all(arrayOfPromises)`. This method is a promise itself, which you use `.then/catch` with. It essentially wait for all promises to be done. _But beware_, if one of the promises fails, the whole array will be rejected. If all are fulfilled, an array will be resolved, with the data at the same index as you placed the promises.

### '.finally'

`.finally(callback)` is a method that can be used with `.then()` and `.catch()` . This function will _always_ be invoked after the promise settled, regardless of the outcome. 

### When to use promises

There is not always useful to use promises. So here is some do's and dont's

**Don't**

* use it when the whole code inside the promise is synchronous.
* use it as a replacement for events that can occur multiple times.
  * A promise is only supposed to fulfill _once_. Not act as a direct callback.
* use it when the code most likely won't finish.
  * Consuming memory by having promises on hold, that is not collected by the garbage collector.

**Do**

* use it when there is some async code, and you need to transform that data, before returning it.
  * For example: REST

### Chaining promises for cleaner code

When you need multiple promises, which takes the result from the last promise and puts it in a new promise.

{% code-tabs %}
{% code-tabs-item title="Example 2" %}
```javascript
somePromiseFunc().then(data => {
    return somePromiseFunc2(data, 'perhaps some extra data')
  }).then((data, someString) => {
    let transformedData = doSomething(data, someString)
    return somePromiseFunc3(transformedData)
  }).then(data => {
    console.log(data)
  }).catch(console.error)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

What if we did not chain these promises? Then it would look a lot more nested, and uglier.

{% code-tabs %}
{% code-tabs-item title="Example 3" %}
```javascript
somePromiseFunc().then(data => {
  somePromiseFunc2(data, 'perhaps some extra data').then((data, someString) => {
    let transformedData = doSomething(data, someString)

    somePromiseFunc3(transformedData).then(data => {
      console.log(data)
    }).catch(console.error)
  }).catch(console.error)
}).catch(console.error)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This almost looks like [callback hell](http://callbackhell.com/), it basically is.

