# implement clearAllTimeout()

`window.setTimeout()` could be used to schedule some task in the future.

Could you implement `clearAllTimeout()` to clear all the timers ? This might be useful when we want to clear things up before page transition.

For example

```js
setTimeout(func1, 10000)
setTimeout(func2, 10000)
setTimeout(func3, 10000)
// all 3 functions are scheduled 10 seconds later
clearAllTimeout()
// all scheduled tasks are cancelled.
```

*note*

You need to keep the interface of `window.setTimeout` and `window.clearTimeout` the same, but you could replace them with new logic

## Solution Approach

To implement `clearAllTimeout` that cancels all the scheduled tasks set by `setTimeout`, you need to keep track of the timeout IDs and clear them when `clearAllTimeout` is called. We can achieve this by overriding the original `window.setTimeout` and `window.clearTimeout` functions to add our custom logic for tracking and clearing timeouts.

Here's how to implement this:

1. **Override `window.setTimeout`**: Wrap the original `window.setTimeout` function to keep track of the timeout IDs.
2. **Override `window.clearTimeout`**: Wrap the original `window.clearTimeout` function to remove the cleared timeout IDs from the tracking list.
3. **Implement `clearAllTimeout`**: Use the list of tracked timeout IDs to clear all the scheduled timeouts.

Here is the implementation:

```javascript
// Store the original setTimeout and clearTimeout functions
const originalSetTimeout = window.setTimeout;
const originalClearTimeout = window.clearTimeout;

// Array to keep track of active timeout IDs
let timeoutIds = [];

// Override window.setTimeout
window.setTimeout = function(callback, delay, ...args) {
  const timeoutId = originalSetTimeout(callback, delay, ...args);
  timeoutIds.push(timeoutId);
  return timeoutId;
};

// Override window.clearTimeout
window.clearTimeout = function(timeoutId) {
  originalClearTimeout(timeoutId);
  timeoutIds = timeoutIds.filter(id => id !== timeoutId);
};

// Implement clearAllTimeout
function clearAllTimeout() {
  timeoutIds.forEach(timeoutId => {
    originalClearTimeout(timeoutId);
  });
  timeoutIds = []; // Clear the list after all timeouts are cleared
}

// Example usage:
const id1 = setTimeout(() => console.log('This will not run'), 10000);
const id2 = setTimeout(() => console.log('This will not run'), 10000);
const id3 = setTimeout(() => console.log('This will not run'), 10000);

clearAllTimeout(); // All scheduled tasks are cancelled.
```

### Explanation:

1. **Override `window.setTimeout`**:
   - Store the original `window.setTimeout` function.
   - Override `window.setTimeout` to keep track of each timeout ID by pushing it to the `timeoutIds` array.
   - Return the timeout ID.

2. **Override `window.clearTimeout`**:
   - Store the original `window.clearTimeout` function.
   - Override `window.clearTimeout` to remove the timeout ID from the `timeoutIds` array when it is cleared.

3. **Implement `clearAllTimeout`**:
   - Iterate over the `timeoutIds` array and clear each timeout using the original `window.clearTimeout`.
   - Reset the `timeoutIds` array to an empty array after all timeouts are cleared.

By doing this, we ensure that all scheduled tasks set by `setTimeout` can be cleared with a single call to `clearAllTimeout`.