# implement curry()

Please implement a `curry()` function, which accepts a function and return a curried one.

Here is an example

```js
const join = (a, b, c) => {
   return `${a}_${b}_${c}`
}
const curriedJoin = curry(join)
curriedJoin(1, 2, 3) // '1_2_3'
curriedJoin(1)(2, 3) // '1_2_3'
curriedJoin(1, 2)(3) // '1_2_3'
```

```js
/**
 * @param { (...args: any[]) => any } fn
 * @returns { (...args: any[]) => any }
 */
function curry(fn) {
  // your code here
}

```

## Solution Approach

### Information we can gather from the example:

```js
const join = (a, b, c) => {
   return `${a}_${b}_${c}`
}
// curry takes a callback function and returns a new function (a closure). 
const curriedJoin = curry(join)

// 1. curriedJoin is a curried version of the join function, meaning it can be called in a chained form.
// 2. The finalization criteria for the currying process are met when the number of arguments passed is sufficient (equal to the original function's arity).
// 3. The spread operator can be used to pass different arguments over multiple calls.
curriedJoin(1, 2, 3) // '1_2_3'
curriedJoin(1)(2, 3) // '1_2_3'
curriedJoin(1, 2)(3) // '1_2_3'
```

Key Words:

1. Closure.
2. Recursion.
3. Spread operator.

### Code

```js
/**
 * @param { (...args: any[]) => any } fn
 * @returns { (...args: any[]) => any }
 */
function curry(fn) {
    // 💡fn = (a, b, c) => {return `${a}_${b}_${c}`}
    return function curried(...args) {
        // 💡fn.length = 3
        if (args.length >= fn.length) {
            // If the parameter length is sufficient, directly call fn with ...args.
            return fn(...args);
        } else {
            // If the parameter length is insufficient,
            // We return a function that wraps curried with ...args and ...nextArgs.
            // It allows us to continue calling the returned function 
            // and pass in the remaining parameters recursively.
            return function(...nextArgs) {
                return curried(...args, ...nextArgs);
            };
        }
    };
}


// Example usage
const join = (a, b, c) => {
  return `${a}_${b}_${c}`;
};
const curriedJoin = curry(join);
console.log(curriedJoin(1, 2, 3)); // '1_2_3'
console.log(curriedJoin(1)(2, 3)); // '1_2_3'
console.log(curriedJoin(1, 2)(3)); // '1_2_3'
```
