# async / await – keywords

`async` and `await` are keywords that were introduced in ES8 \(ES2017\). These defines an asynchronous function. Only a async function can contain the `await` keyword. The `await` keyword is placed in front of a promise or a async function, to pause the execution of where it was called, and wait for the promise or async function to complete its task. _**Please not that this is not supported in most browsers, and most likely need a compiler/transpiler like Babel to run.**_

### Examples

{% code-tabs %}
{% code-tabs-item title="Example 1" %}
```javascript
async function someAsyncFunc() {
    // somePromiseFunc returns a promise in this example
    const someResult = await somePromiseFunc()
    
    return someResult
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Example 2" %}
```javascript
async function someAsyncFunc() {
    let status = 'ok'
    
    try {
        await doSomeImportantAsyncWork()
    } catch(e) {
        status = e
    }
    
    return {
        status
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Example 3" %}
```javascript
async function someAsyncFunction() {
    const response = await someBadRequest().catch(console.error)
    
    if (response) {
        return response
    } else {
        return {
            err: 'Something went terribly wrong.'
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Error handling

Look at examples 2 and 3. When working with promises you could easily attach a `.catch()` at the promise chain. You could also wrapping `await` statements inside a `try/catch` block too. You could alternatively append a `.catch()` to the promise you put an `await` in front of _\(example 3, line 2\)_. But since async functions it self are being wrapped in a promise behind the curtains. This means that you can also do this:

{% code-tabs %}
{% code-tabs-item title="Example  4" %}
```javascript
// This will reject after 3 seconds
function timerThing() {
  return new Promise((resolve, reject) => {
    setTimeout(() => reject('kakadoo'), 3 * 1000)
  })
}

async function someFunction() {
  await timerThing()
}

someFunction().catch(console.error) // Output: kakadoo
```
{% endcode-tabs-item %}
{% endcode-tabs %}

