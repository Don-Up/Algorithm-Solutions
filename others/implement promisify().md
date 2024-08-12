#  implement promisify()

<audio src="assets/implement%20promisify().mp3"></audio>

Let's take a look at following error-first callback.

```js
const callback = (error, data) => {
  if (error) {
    // handle the error
  } else {
    // handle the data
  }
}
```

Now think about async functions that takes above error-first callback as last argument.

```js
 const func = (arg1, arg2, callback) => {
  // some async logic
  if (hasError) {
    callback(someError)
  } else {
    callback(null, someData)
  }
}
```

You see what needs to be done now. Please **implement promisify()** to make the code better.

```js
const promisedFunc = promisify(func)

promisedFunc().then((data) => {
  // handles data
}).catch((error) => {
  // handles error
})
```

## Solution Approach

To convert a callback-based function to a promise-based function using `promisify`, we need to wrap the original function in a new function that returns a promise. This new function will:

1. Take the same arguments as the original function, except for the callback.
2. Return a new `Promise`.
3. Inside the promise, call the original function with the provided arguments and an additional callback.
4. The additional callback will resolve or reject the promise based on the error-first convention:
   - If there is an error (the first argument is truthy), reject the promise.
   - If there is no error (the first argument is falsy), resolve the promise with the data.

Here is a detailed step-by-step breakdown:

1. **Return a new function**:
   - This function takes the same arguments as the original function, except for the callback.
2. **Return a new `Promise`**:
   - Inside this new function, we return a new `Promise`.
3. **Call the original function**:
   - Use `func.apply` to call the original function with the provided arguments and an additional callback.
4. **Handle the callback**:
   - The additional callback will resolve or reject the promise based on the error-first convention:
     - If there is an error (the first argument is truthy), reject the promise with the error.
     - If there is no error (the first argument is  ), resolve the promise with the data.

## Full Code

```js
/**
 * @param {(...args) => void} func
 * @returns {(...args) => Promise<any>}
 */
function promisify(func) {
  // Return a new function that returns a Promise
  return function(...args) {
    return new Promise((resolve, reject) => {
      // Call the original function with the provided arguments and an additional callback
      func.apply(this, [...args, (error, data) => {
        if (error) {
          // Reject the promise if there is an error
          reject(error);
        } else {
          // Resolve the promise with the data
          resolve(data);
        }
      }]);
    });
  };
}
```

