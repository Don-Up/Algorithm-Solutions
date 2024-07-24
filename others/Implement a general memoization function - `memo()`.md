# Implement a general memoization function - `memo()`

[Memoization](https://whatthefuck.is/memoization) is a common technique to boost performance. If you use React, you definitely have used `React.memo` before.

Memoization is also commonly used in algorithm problem, when you have a recursion solution, in most cases, you can improve it by memoization, and then you might be able to get a Dynamic Programming approach.

So could you implement a general `memo()` function, which caches the result once called, so when same arguments are passed in, the result will be returned right away.

```js
const func = (arg1, arg2) => {
  return arg1 + arg2
}

const memoed = memo(func)

memoed(1, 2) 
// 3, func is called

memoed(1, 2) 
// 3 is returned right away without calling func

memoed(1, 3)
// 4, new arguments, so func is called
```

The arguments are arbitrary, so memo should accept an extra resolver parameter, which is used to generate the cache key, like what [_.memoize()](https://lodash.com/docs/4.17.15#memoize) does.

```js
const memoed = memo(func, () => 'samekey')

memoed(1, 2) 
// 3, func is called, 3 is cached with key 'samekey'

memoed(1, 2) 
// 3, since key is the same, 3 is returned without calling func

memoed(1, 3) 
// 3, since key is the same, 3 is returned without calling func
```

Default cache key could be just `Array.from(arguments).join('_')`

*note*

It is a trade-off of space for time, so if you use this in an interview, please do analyze how much space it might cost.

## Solution Approach

To implement the cache feature, you usually need a map and methods to handle the storage and retrieval of cached data.

The `memo` function is essentially a closure. We can declare a map called `cache` and a `defaultResolver` within the outer function.

Referring to the implementation of `defaultResolver`, we can use `join` to merge the `args` array into a single string that represents a unique key.

```js
function memo(func, resolver) {
  const cache = new Map();

  // Default resolver function
  const defaultResolver = (...args) => args.join('_');
    
  return function(...args){
      // todo
  }
}
```

In the inner function, we first need to get the key based on `args` and `resolver`. If `resolver` is provided, we call `resolver` with `...args`; otherwise, we call `defaultResolver` with `...args`.

```js
const key = resolver ? resolver(...args) : defaultResolver(...args);
```

Once we have the key, we should determine if the cache contains it. If it does, we return `cache.get(key)` directly.

```js
if (cache.has(key)) {
  return cache.get(key);
}
```

Otherwise, we should call func, cache its result and return result.

```js
const result = func.apply(this, args);
cache.set(key, result);
return result;
```

## Full Code

```js
/**
 * @param {Function} func
 * @param {(args:[]) => string } [resolver] - cache key generator
 */
function memo(func, resolver) {
  const cache = new Map();

  // Default resolver function
  const defaultResolver = (...args) => args.join('_');

  return function(...args) {
    // Use resolver to get the cache key if passed, otherwise use defaultResolver
    const key = resolver ? resolver(...args) : defaultResolver(...args);

    if (cache.has(key)) {
      return cache.get(key);
    }

    const result = func.apply(this, args);
    cache.set(key, result);
    return result;
  };
}
```

