# implement Array.prototype.flat()

There is already [Array.prototype.flat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat) in JavaScript (ES2019), which reduces the nesting of Array.

Could you manage to implement your own one?

Here is an example to illustrate

```js
const arr = [1, [2], [3, [4]]];
flat(arr)
flat(arr, 1)
flat(arr, 2)

```

**follow up**

Are you able to solve it both recursively and iteratively?

## Solution Approach

To implement our own version of `Array.prototype.flat()`, we need to handle nested arrays and flatten them to a specified depth. We can solve this problem using both recursive and iterative approaches.

### Recursive Approach

Here’s the refined version with grammatical corrections and clarifications:

---

#### Thinking

First, we can implement a lite version of **flattening**:

```js
function flat(arr) {
    // Use `reduce` to iterate over `arr` for more convenient concatenation.
    return arr.reduce((acc, val) => {
        if (Array.isArray(val)) {
            // If `val` is an array, we recursively flatten and spread it into `acc`.
            acc.push(...flat(val));
        } else {
            // If `val` is a non-array value, push it directly.
            acc.push(val);
        }
        return acc;
    }, []);
}
```

Next, we can consider the flattening depth:

```js
function flat(arr, depth = 1) {
  // If the flattening depth requirement has been met, return `arr` as is.
  if (depth < 1) return arr;

  return arr.reduce((acc, val) => {
    if (Array.isArray(val)) {
      // For each recursion, decrement the depth by one.
      acc.push(...flat(val, depth - 1));
    } else {
      acc.push(val);
    }
    return acc;
  }, []);
}
```

#### Code

```js
function flat(arr, depth = 1) {
  if (depth < 1) return arr;

  return arr.reduce((acc, val) => {
    if (Array.isArray(val)) {
      acc.push(...flat(val, depth - 1));
    } else {
      acc.push(val);
    }
    return acc;
  }, []);
}

// Example usage
const arr = [1, [2], [3, [4]]];
console.log(flat(arr)); // [1, 2, 3, [4]]
console.log(flat(arr, 1)); // [1, 2, 3, [4]]
console.log(flat(arr, 2)); // [1, 2, 3, 4]
```

### Iterative Approach

The iterative approach uses a stack to keep track of the elements and their depths. This avoids the function call overhead and potential stack overflow issues with deeply nested arrays.

Here's the implementation:

```js
function flatIterative(arr, depth = 1) {
  const stack = [...arr.map(item => [item, depth])];
  const result = [];

  while (stack.length > 0) {
    const [current, currentDepth] = stack.pop();

    if (Array.isArray(current) && currentDepth > 0) {
      stack.push(...current.map(item => [item, currentDepth - 1]));
    } else {
      result.push(current);
    }
  }

  return result.reverse();
}

// Example usage
console.log(flatIterative(arr)); // [1, 2, 3, [4]]
console.log(flatIterative(arr, 1)); // [1, 2, 3, [4]]
console.log(flatIterative(arr, 2)); // [1, 2, 3, 4]
```

### Full Code with Both Approaches

```js
// Recursive approach
function flat(arr, depth = 1) {
  if (depth < 1) return arr;

  return arr.reduce((acc, val) => {
    if (Array.isArray(val)) {
      acc.push(...flat(val, depth - 1));
    } else {
      acc.push(val);
    }
    return acc;
  }, []);
}

// Iterative approach
function flatIterative(arr, depth = 1) {
  const stack = [...arr.map(item => [item, depth])];
  const result = [];

  while (stack.length > 0) {
    const [current, currentDepth] = stack.pop();

    if (Array.isArray(current) && currentDepth > 0) {
      stack.push(...current.map(item => [item, currentDepth - 1]));
    } else {
      result.push(current);
    }
  }

  return result.reverse();
}

// Example usage
const arr = [1, [2], [3, [4]]];
console.log(flat(arr)); // [1, 2, 3, [4]]
console.log(flat(arr, 1)); // [1, 2, 3, [4]]
console.log(flat(arr, 2)); // [1, 2, 3, 4]

console.log(flatIterative(arr)); // [1, 2, 3, [4]]
console.log(flatIterative(arr, 1)); // [1, 2, 3, [4]]
console.log(flatIterative(arr, 2)); // [1, 2, 3, 4]
```

Both approaches effectively flatten the array to the specified depth. The recursive approach is straightforward and easy to understand, while the iterative approach can handle deeper nesting without the risk of a stack overflow.