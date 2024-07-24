# [Product of Array Except Self](https://leetcode.cn/problems/product-of-array-except-self/)

Given an integer array `nums`, return *an array* `answer` *such that* `answer[i]` *is equal to the product of all the elements of* `nums` *except* `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

 

**Example 1:**

```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

**Example 2:**

```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

 ## Solution Approach

To solve the problem, we can use the concepts of prefix and suffix products.

1. Prefix Product: Create an array `left`, where `left[i]` represents the product of all elements before the index `i` (excluding `i`) of the array `nums`.
1. Suffix Product: Create an array `left`, where `left[i]` represents the product of all elements after the index `i` (excluding `i`) of the array `nums`.
1. Resulting Array: For each index `i`, the resulting array `answer[i]` is equal to `left[i]` multiplied by `right[i]`.

### Implementation Steps

1. Initialize two arrays, `left` and `right`, each with a length of `n`, and the resulting array `answer`.
2. Calculate `left`: Initialize `left[0]` to 1 because there is no element to the left of the first element. For each `i`, `left[i]` is equal to `left[i-1]` multiplied by `nums[i-1]`.
3. Calculate `right`: Initialize `right[0]` to 1 because there is no element to the right of the first element. For each `i`, `right[i]` is equal to `left` multiplied by `nums[i-1]`.
4. Calculate the resulting array: For each `i`, `answer[i]` is equal to `left[i]` multiplied by `right[i]`.

### Example Code

 ```js
 /**
  * @param {number[]} nums
  * @return {number[]}
  */
 var productExceptSelf = function(nums) {
     const n = nums.length;
     const left = new Array(n).fill(1);
     const right = new Array(n).fill(1);
     const answer = new Array(n).fill(1);
 
     // Calculate left products
     for (let i = 1; i < n; i++) {
         left[i] = left[i - 1] * nums[i - 1];
     }
 
     // Calculate right products
     for (let i = n - 2; i >= 0; i--) {
         right[i] = right[i + 1] * nums[i + 1];
     }
 
     // Calculate the result
     for (let i = 0; i < n; i++) {
         answer[i] = left[i] * right[i];
     }
 
     return answer;
 };
 
 // Example Invocation
 console.log(productExceptSelf([1,2,3,4])); // Output：[24,12,8,6]
 console.log(productExceptSelf([-1,1,0,-3,3])); // Output：[0,0,9,0,0]
 
 ```

### Optimize the space complexity

We can solve the problem without using extra space by using only the resulting array `answer` and directly updating it when calculating the suffix product.

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function(nums) {
    const n = nums.length;
    const answer = new Array(n).fill(1);

    // Calculate left products and store in answer
    for (let i = 1; i < n; i++) {
        answer[i] = answer[i - 1] * nums[i - 1];
    }

    // Calculate right products and update answer
    let right = 1;
    for (let i = n - 1; i >= 0; i--) {
        answer[i] = answer[i] * right;
        right = right * nums[i];
    }

    return answer;
};

// Example Invocation
console.log(productExceptSelf([1, 2, 3, 4])); // Output：[24,12,8,6]
console.log(productExceptSelf([-1, 1, 0, -3, 3])); // Output：[0,0,9,0,0]
```

In the optimized version, we first calculate the prefix product and store it in `answer`. Then, we maintain the suffix product using a variable `right`, updating `answer` step by step. This approach reduces the space complexity from O(n) to O(1) (excluding the space used by `answer`).