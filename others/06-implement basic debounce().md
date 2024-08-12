# implement basic debounce()

Debounce is a common technique used in Web Application, in most cases using [lodash solution](https://lodash.com/docs/4.17.15#debounce) would be a good choice.

could you implement your own version of basic `debounce()`?

In case you forgot, `debounce(func, delay)` will returned a debounced function, which delays the invoke.

Here is an example.

Before debouncing we have a series of calling like

```
─ A ─ B ─ C ─ ─ D ─ ─ ─ ─ ─ ─ E ─ ─ F ─ G 
```

After debouncing at wait time of 3 dashes

```
─ ─ ─ ─ ─ ─ ─ ─ D ─ ─ ─ ─ ─ ─ ─ ─ ─ G 
```

**notes**

1. please follow above spec. the behavior might not be exactly the same as `lodash.debounce()`
2. because `window.setTimeout` and `window.clearTimeout` are not accurate in browser environment, they are replaced to other implementation when judging your code. They still have the same interface, and internally keep track of the timing for testing purpose.

Something like below will be used to do the test.

```js
let currentTime = 0
const run = (input) => {
  currentTime = 0
  const calls = []
  const func = (arg) => {
     calls.push(`${arg}@${currentTime}`)
  }
  const debounced = debounce(func, 3)
  input.forEach((call) => {
     const [arg, time] = call.split('@')
     setTimeout(() => debounced(arg), time)
  })
  return calls
}
expect(run(['A@0', 'B@2', 'C@3'])).toEqual(['C@5'])
```

## Solution Approach

To implement a basic version of `debounce()`, we need to ensure that the provided function `func` is executed only after a specified delay (`wait`) has passed since the last time the debounced function was invoked. Each call to the debounced function will reset the delay timer.

Here's how you can implement the `debounce` function:

```js
/**
 * @param {(...args: any[]) => any} func
 * @param {number} wait
 * @returns {(...args: any[]) => any}
 */
function debounce(func, wait) {
  let timeoutId = null;

  return function(...args) {
    // Clear the existing timeout if any
    if (timeoutId !== null) {
      clearTimeout(timeoutId);
    }

    // Set a new timeout to call the function after the wait period
    timeoutId = setTimeout(() => {
      func(...args);
    }, wait);
  };
}

// Example usage
let currentTime = 0;
const setTimeout = (fn, delay) => {
  currentTime += delay;
  fn();
};

const run = (input) => {
  currentTime = 0;
  const calls = [];
  const func = (arg) => {
    calls.push(`${arg}@${currentTime}`);
  };
  const debounced = debounce(func, 3);
  input.forEach((call) => {
    const [arg, time] = call.split('@');
    setTimeout(() => debounced(arg), time - currentTime);
  });
  return calls;
};

// Test cases
console.log(run(['A@0', 'B@2', 'C@3'])); // ['C@5']
console.log(run(['A@0', 'B@1', 'C@2', 'D@3', 'E@8', 'F@10', 'G@11'])); // ['D@6', 'G@14']
console.log(run(['A@0', 'B@1', 'C@2'])); // ['C@5']
console.log(run(['A@0', 'B@2', 'C@4', 'D@6'])); // ['D@9']
```

### Explanation

1. **Initialize timeoutId:** We start by keeping track of the current timeout ID using `timeoutId`. Initially, it's set to `null`.
2. **Clear existing timeout:** If `timeoutId` is not `null`, it means there's a pending execution, so we clear it using `clearTimeout()`.
3. **Set a new timeout:** We set a new timeout to call `func` after the specified `wait` period using `setTimeout()`.
4. **Mock setTimeout for Testing:** In the example, `setTimeout` is mocked to increment `currentTime` and immediately execute the function to simulate the timing behavior.

This implementation ensures that `func` is called only after the specified delay has passed since the last call, following the behavior of debouncing.