#  implement `_.once()`

[_.once(func)](https://lodash.com/docs/4.17.15#once) is used to force a function to be called only once, later calls only returns the result of first call.

Can you implement your own `once()`?

```js
function func(num) {
  return num
}

const onced = once(func)

onced(1) 
// 1, func called with 1

onced(2)
// 1, even 2 is passed, previous result is returned 
```

<audio src="assets/implement%20%60_.once()%60.mp3"></audio>

## Solution Approach

To implement a function that can be called only once, we need to use closures to maintain a variable `isCalled` that indicates whether `func` has been called, as well as a variable `result` to store the result of the first call.

In the inner function, we check if `isCalled` is false. If so, we reassign it to `true`. Then we call `func.apply` with `this` and `args` and assign its return value to `result`, 

Finally, we return `result` to complete the `once` function.

## Full Code

```js
/**
 * @param {Function} func
 * @return {Function}
 */
function once(func) {
  // your code here
  let isCalled = false
  let result = null
  return function(...args){
    if(!isCalled){
      isCalled = true
      result = func.apply(this, args)
    }
    return result
  }
}
```

