# Hoisting

### Definition

> Hoisting is a behaviour in which \(function and variable\) declarations are moved to the top of their scope.

### Variable hoisting

Here is a couple of examples of how hoisting works for _variables_.  
Concider this code:

{% code-tabs %}
{% code-tabs-item title="Example 1" %}
```javascript
someFunction()

let x = 100
```
{% endcode-tabs-item %}
{% endcode-tabs %}

However, this is how the code is looks like for the interpreter.

{% code-tabs %}
{% code-tabs-item title="Example 1 - Interpreter" %}
```javascript
let x

someFunction()

x = 100
```
{% endcode-tabs-item %}
{% endcode-tabs %}

As you can see, the code is somewhat the same, however the joint declaration and assignment at line 3 in the first code block, is now separated. The declaration of _x_ is hoisted to the top it's scope, while the assignment stays where it was originally.

### Function hoisting

Functions, like variables, are also hoisted to the top. However only _function declarations_, and not _function expressions_.

{% code-tabs %}
{% code-tabs-item title="Example 2" %}
```javascript
someFunction()       // Outputs: 'I am hoisted!'
anotherFunction()    // TypeError: undefined is not a function.

// Function declaration
function someFunction() {
    console.log('I am hoisted!')
}

// Function expression
let anotherFunction = () => {
    console.log('I am not hoisted :(')
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Example 2 - Interpreter" %}
```javascript
// Hoisted function declaration
function someFunction() {
    console.log('I am hoisted!')
}

// Hoisted declaration
let anotherFunction

someFunction()       // Outputs: 'I am hoisted!'
anotherFunction()    // TypeError: undefined is not a function.

// Assignemnt for function expression
anotherFunction = () => {
    console.log('I am not hoisted :(')
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

_someFunction_ is hoisted to the top of the scope. However, since _anotherFunction_ is a variable, it will then be hoisted as if it was a variable. Therefore, the actual assignment of the function expression, _anotherFunction_, is assigned where it was initially declared.

### Mixed examples

Here are some examples when both a function and a variable is sharing the name/identifier.

{% code-tabs %}
{% code-tabs-item title="Example 3" %}
```javascript
function someFunction() {
    let x = 'some string'
    
    function x() {
        return 'I am inside a nested function'
    }
    
    return x()
}

console.log(someFunction() // Chrome: TypeError: x is not a function
                           // Node 9.x: SyntaxError: Identifier 'x' has already been declared
```
{% endcode-tabs-item %}
{% endcode-tabs %}

As mentioned, both the variable _x_ and function _x_ is sharing identifiers. In this case, the interpreter "_ignores"_ the variable hoisting. But why is this still producing an error? Consider it from the interpreter's side of view.

{% code-tabs %}
{% code-tabs-item title="Example 3 - Interpreter" %}
```javascript
function someFunction() {
    // let x – IGNORED
    
    function x() {
        return 'I am inside a nested function'
    }
    
    // This line breaks the code.
    x = 'some string'
    
    return x()
}

console.log(someFunction())
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If the interpreter does not complain about the colliding identifier declaration \(that both the function and the variable is trying to reserve _x_\), it will atleast complain about that _x_ is not a function. Why? Because the variable hoisting is ignored, then _x_ will be assigned as a function. You are not able to redeclare a function to a variable. Since the second declaration is a string, it will complain about _x_ is not a function. However, this example will work:

{% code-tabs %}
{% code-tabs-item title="Example 4 " %}
```javascript
function someFunction() {
    // You can actually redeclare functions like this.
    x = () => 'This redeclaration will work'
    
    function x() {
        return 'I am inside a nested function'
    }
    
    return x()    
}

console.log(someFunction()) // Output: This redeclaration will work
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Example 4 – Interpreter" %}
```javascript
function someFunction() {
    function x() {
        return 'I am inside a nested function'
    }
    
    // You can actually redeclare functions like this.
    x = () => 'This redeclaration will work'
    
    return x()
}

console.log(someFunction()) // Output: This redeclaration will work
```
{% endcode-tabs-item %}
{% endcode-tabs %}

