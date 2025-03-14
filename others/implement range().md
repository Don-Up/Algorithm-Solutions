# implement range()

<audio src="assets/implement%20range().mp3"></audio>

Can you create a `range(from, to)` which makes following work?

For example:

When using a for of loop to iterate over the range from 1 to 4, it should log the numbers 1, 2, 3, and 4.

```js
for (let num of range(1, 4)) {
  console.log(num)  
}
// 1
// 2
// 3
// 4
```

This is a simple one, could you think **more fancy approaches other than for-loop**?

Notice that you are not required to return an array, but something [iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterator_protocol) would be fine.

## Solution Approach

To create a `range` function that allows iteration over a sequence of numbers, we can implement the iterable protocol in JavaScript. This involves creating an object with a `[Symbol.iterator]` method that returns an iterator.

Here's how we can implement this:

### Implementation

```javascript
/**
 * @param {number} from
 * @param {number} to
 * @return {Object}
 */
function range(from, to) {
  return {
    [Symbol.iterator]() {
      let current = from;
      return {
        next() {
          if (current <= to) {
            return { value: current++, done: false };
          } else {
            return { done: true };
          }
        }
      };
    }
  };
}

// Example usage:
for (let num of range(1, 4)) {
  console.log(num);
}
// Output:
// 1
// 2
// 3
// 4
```

### Explanation

1. **Range Function**:
   - The `range` function takes two parameters: `from` and `to`.
   - It returns an object that has a `[Symbol.iterator]` method.

2. **Iterable Protocol**:
   - The `[Symbol.iterator]` method returns an iterator object.
   - The iterator object has a `next` method which:
     - Returns the next value in the range if the current value is less than or equal to `to`.
     - Increments the current value.
     - Returns `{ done: true }` when the iteration is complete.

### Alternative Approaches

#### Using a Generator Function
A more elegant and concise way to achieve this is by using a generator function, which inherently supports the iterable protocol:

```javascript
/**
 * @param {number} from
 * @param {number} to
 * @return {Generator}
 */
function* range(from, to) {
  for (let i = from; i <= to; i++) {
    yield i;
  }
}

// Example usage:
for (let num of range(1, 4)) {
  console.log(num);
}
// Output:
// 1
// 2
// 3
// 4
```

### Explanation of Generator Function

1. **Generator Function**:
   - The `range` function is defined with an asterisk (`function*`), making it a generator function.
   - The `yield` keyword is used to produce a sequence of values.
   - The `for...of` loop consumes the values yielded by the generator.

Both approaches fulfill the requirement of creating an iterable that produces a range of numbers from `from` to `to`. The generator function is a more concise and idiomatic way to create such iterables in JavaScript.