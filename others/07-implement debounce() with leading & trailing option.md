# implement debounce() with leading & trailing option

This is a follow up on [6. implement basic debounce()](https://bigfrontend.dev/problem/implement-basic-debounce), please refer to it for detailed explanation.

In this problem, you are asked to implement an enhanced `debounce()` which accepts third parameter, `option: {leading: boolean, trailing: boolean}`

1. leading: whether to invoke right away
2. trailing: whether to invoke after the delay.

[6. implement basic debounce()](https://bigfrontend.dev/problem/implement-basic-debounce()) is the default case with `{leading: false, trailing: true}`.

for the previous example of debouncing by 3 dashes

```
─ A ─ B ─ C ─ ─ D ─ ─ ─ ─ ─ ─ E ─ ─ F ─ G 
```

with {leading: false, trailing: true}, we get as below

```
─ ─ ─ ─ ─ ─ ─ ─ D ─ ─ ─ ─ ─ ─ ─ ─ ─ G
```

with {leading: true, trailing: true}:

```
─ A ─ ─ ─ ─ ─ ─ ─ D ─ ─ ─ E ─ ─ ─ ─ ─ ─ G
```

with {leading: true, trailing: false}

```
─ A ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ E
```

with {leading: false, trailing: false}, of course, nothing happens.

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
expect(run(['A@0', 'B@2', 'C@3'])).toEqual(['C@6'])
```

## Solution Approach

To implement the `debounce` function with `leading` and `trailing` options, we need to handle the conditions where the function can be called immediately on the leading edge, and/or after the wait period on the trailing edge. Here is the solution:

```js
/**
 * @param {(...args: any[]) => any} func
 * @param {number} wait
 * @param {Object} option
 * @param {boolean} option.leading
 * @param {boolean} option.trailing
 * @returns {(...args: any[]) => any}
 */
function debounce(func, wait, option = { leading: false, trailing: true }) {
  let timeoutId = null;
  let lastArgs = null;
  let lastThis = null;
  let result = null;
  let lastCallTime = 0;

  const { leading, trailing } = option;

  const invokeFunc = () => {
    result = func.apply(lastThis, lastArgs);
    lastThis = lastArgs = null;
  };

  const startTimer = (callback, delay) => {
    if (timeoutId) clearTimeout(timeoutId);
    timeoutId = setTimeout(callback, delay);
  };

  const shouldInvoke = (time) => {
    const timeSinceLastCall = time - lastCallTime;
    return lastCallTime === 0 || timeSinceLastCall >= wait;
  };

  const trailingEdge = (time) => {
    timeoutId = null;
    if (trailing && lastArgs) {
      invokeFunc();
      lastCallTime = time;
    }
  };

  return function (...args) {
    const time = Date.now();
    const isInvoking = shouldInvoke(time);

    lastArgs = args;
    lastThis = this;

    if (isInvoking) {
      if (leading) {
        invokeFunc();
      }
      lastCallTime = time;
      if (trailing) {
        startTimer(() => trailingEdge(time), wait);
      }
    } else if (trailing) {
      startTimer(() => trailingEdge(time), wait);
    }

    return result;
  };
}

// Example usage for testing
let currentTime = 0;
const setTimeout = (fn, delay) => {
  currentTime += delay;
  fn();
};

const run = (input, options) => {
  currentTime = 0;
  const calls = [];
  const func = (arg) => {
    calls.push(`${arg}@${currentTime}`);
  };
  const debounced = debounce(func, 3, options);
  input.forEach((call) => {
    const [arg, time] = call.split('@');
    setTimeout(() => debounced(arg), time - currentTime);
  });
  return calls;
};

// Test cases
console.log(run(['A@0', 'B@2', 'C@3'], { leading: false, trailing: true })); // ['C@6']
console.log(run(['A@0', 'B@2', 'C@3', 'D@6'], { leading: true, trailing: true })); // ['A@0', 'D@9']
console.log(run(['A@0', 'B@2', 'C@3'], { leading: true, trailing: false })); // ['A@0']
console.log(run(['A@0', 'B@2', 'C@3'], { leading: false, trailing: false })); // []
```

### Explanation:

1. **Initialization:** We initialize `timeoutId`, `lastArgs`, `lastThis`, `result`, and `lastCallTime`.

2. **Invoke Function:** A helper function `invokeFunc` to call `func` with the latest context and arguments.

3. **Start Timer:** A helper function `startTimer` to manage the `setTimeout` calls.

4. **Should Invoke:** A helper function `shouldInvoke` to check if the function should be called based on the time since the last call.

5. **Trailing Edge:** A helper function `trailingEdge` to handle the trailing call logic.

6. **Main Function:** The returned debounced function handles the logic for invoking `func` based on the `leading` and `trailing` options.

This implementation respects the behavior specified in the problem statement and should work correctly for the given test cases.