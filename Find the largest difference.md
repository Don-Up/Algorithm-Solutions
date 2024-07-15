# Find the largest difference

Given an array of numbers, pick any two numbers `a` and `b`, we could get the difference by `Math.abs(a - b)`.

Can you write a function to get the largest difference?

```js
largestDiff([-1, 2,3,10, 9])
// 11,  obviously Math.abs(-1 - 10) is the largest

largestDiff([])
// 0

largestDiff([1])
// 0
```

## Solution Approach

To find the largest difference in a number array, we just need to find the maximum and the minimum values, and calculate the difference between them.

First of all, we need to handle edge cases. If the length of `arr` is less than or equal to 1, we simply return 0.

After that, we can declare two variables: `min`, initialized to `Infinity`, and `max`, initialized to `-Infinity`.

Then we can start a `for...of` loop on `arr`. In each iteration, if `num` is less than `min`, we update `min`; and if `num` is greater than `max`, we update `max`.

Finally, we can end the function by returning `max - min`.

## Full Code

```js
/**
 * @param {number[]} arr
 * @return {number}
 */
function largestDiff(arr) {
  // your code here
  if(arr.length <= 1){
    return 0
  }
  let min = Infinity
  let max = -Infinity
  for(num of arr){
    if(num<min){
      min = num
    }
    if(num>max){
      max = num
    }
  }
  return max-min
}
```

