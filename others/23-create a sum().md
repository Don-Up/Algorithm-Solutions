# create a sum()

Create a `sum()`, which makes following possible

```js
const sum1 = sum(1)
sum1(2) == 3 // true
sum1(3) == 4 // true
sum(1)(2)(3) == 6 // true
sum(5)(-1)(2) == 6 // true
```

> #### Thinking🤔
>
> ```js
> sum(1)(2) == 3 // true
> sum(1)(3) == 4 // true
> sum(1)(2)(3) == 6 // true
> sum(5)(-1)(2) == 6 // true
> ```
>
> The number of chained calls in currying is not fixed, so we cannot directly return a value; we can only return a function. To solve this, we can define a custom `valueOf` method to convert the function to the final result when its return value is accessed.

## Solution Approach

<audio src="assets/create%20a%20sum.mp3"></audio>

To create a `sum` function that supports chaining, we need to return a function that keeps track of the current sum and continues to return itself to allow further chaining. Additionally, we need to define a custom `toString` or `valueOf` method to convert the function to the final value when necessary.

Here's the implementation:

```js
/**
 * @param {number} num
 */
function sum(num) {
  const innerSum = (currentSum) => {
    // use a closure (`innerSum`) to accumulate the sum. Each call to the `next` function updates the accumulated sum.
    const next = (nextNum) => innerSum(currentSum + nextNum);
    // override the `valueOf` method of the `next` function to return the current accumulated sum.
    next.valueOf = () => currentSum;
    // The `next` function returns itself (`next`) to enable chaining.
    return next;
  };

  return innerSum(num);
}

// Usage examples:
const sum1 = sum(1);
console.log(sum1(2) == 3); // true
console.log(sum1(3) == 4); // true
console.log(sum(1)(2)(3) == 6); // true
console.log(sum(5)(-1)(2) == 6); // true
```

### Explanation:
1. **Closure for Accumulation**: We use a closure (`innerSum`) to accumulate the sum. Each call to the `next` function updates the accumulated sum.
2. **Function Returning Itself**: The `next` function returns itself (`next`) to enable chaining.
3. **Custom `valueOf` Method**: We override the `valueOf` method of the `next` function to return the current accumulated sum. This allows the function to be coerced into a number when using comparison operators like `==`.

### Testing:
You can test the implementation with the provided usage examples. The `==` operator implicitly calls the `valueOf` method, allowing the comparison to work as expected.