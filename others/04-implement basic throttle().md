# implement basic throttle()

Throttling is a common technique used in Web Application, in most cases using [lodash solution](https://lodash.com/docs/4.17.15#throttle) would be a good choice.

could you implement your own version of basic `throttle()`?

In case you forgot, `throttle(func, delay)` will return a throttled function, which will invoke the func at a max frequency no matter how throttled one is called.

Here is an example.

Before throttling we have a series of calling like

```
─ A ─ B ─ C ─ ─ D ─ ─ ─ ─ ─ ─ E ─ ─ F ─ G
```

After throttling at wait time of 3 dashes

```
─ A ─ ─ ─ C ─ ─ ─D ─ ─ ─ ─ E ─ ─ ─ G 
```

Be aware that

- call A is triggered right way because not in waiting time
- function call B is swallowed because B, C is in the cooling time from A, and C is latter.

**notes**

1. please follow above spec. the behavior is not exactly the same as `lodash.throttle()`
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
  const throttled = throttle(func, 3)
  input.forEach((call) => {
     const [arg, time] = call.split('@')
     setTimeout(() => throttled(arg), time)
  })
  return calls
}
expect(run(['A@0', 'B@2', 'C@3'])).toEqual(['A@0', 'C@3'])
```

## Solution Approach

To implement a basic version of `throttle()`, we need to ensure that the provided function `func` is executed at most once every `wait` milliseconds. This implementation will call `func` immediately when the throttled function is first invoked, then ignore any subsequent calls until the `wait` period has elapsed.

Here's how you can implement the `throttle` function:

```js
/**
 * @param {(...args:any[]) => any} func
 * @param {number} wait
 * @returns {(...args:any[]) => any}
 */
function throttle(func, wait) {
  let lastExecutionTime = 0;

  return function(...args) {
    const now = Date.now();

    if (now - lastExecutionTime >= wait) {
      lastExecutionTime = now;
      func(...args);
    }
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
  const throttled = throttle(func, 3);
  input.forEach((call) => {
    const [arg, time] = call.split('@');
    setTimeout(() => throttled(arg), time - currentTime);
  });
  return calls;
};

console.log(run(['A@0', 'B@2', 'C@3'])); // ['A@0', 'C@3']
console.log(run(['A@0', 'B@1', 'C@2', 'D@3', 'E@8', 'F@10', 'G@11'])); // ['A@0', 'D@3', 'E@8', 'G@11']
```

### Explanation

1. **Initialize lastExecutionTime:** We start by keeping track of the last time the `func` was executed using `lastExecutionTime`. Initially, it's set to 0.
2. **Return a throttled function:** The returned function will check the current time (`now`) against `lastExecutionTime`. If the time difference is greater than or equal to `wait`, it will execute `func` and update `lastExecutionTime`.
3. **Mock setTimeout for Testing:** In the example, `setTimeout` is mocked to increment `currentTime` and immediately execute the function to simulate the timing behavior.

This implementation ensures that `func` is not called more than once within the specified `wait` time, meeting the basic requirements of throttling.