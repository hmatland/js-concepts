# Generators

Generator function are function which we can control the iteration, and apply custom actions per iteration, in a pretty way. Generators are declared by the `function*` keyword.

A nice feature that generators have, is that you can call `.next(args)` on the function to get the next value, and that it's internal state remains through out the usage of it. I found an good example from [here](https://gist.github.com/jfairbank/8d36e4bde9c16dc0bac7),  for Fibonacci numbers. I did somewhat modify it:

{% code-tabs %}
{% code-tabs-item title="Example 1 - Fibonacci" %}
```javascript
function* fibonacci(n, current = 0, next = 1) {
    if (n === 0) {
      return current
    }

    yield current
    yield *fibonacci(n - 1, next, current + next)
}

const [...fibo] = fibonacci(10)
console.log(fibo) // Output: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This is a recursive version of Fibonacci, with a generator. If it looks confusing, then I'll try to explain it. The parameter `n` specifies how many numbers in the Fibonacci series you want. For every iteration, at line 7 it takes n and decrement it by 1, and passes the decremented n as an argument, to a recursive function. When `n` reaches 0, it will finally `return` and therefore stopping the generator.

To those who are wondering that the `=` at the parameters is, it's [a default parameter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters). 

