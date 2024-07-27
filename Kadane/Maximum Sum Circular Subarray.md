# [Maximum Sum Circular Subarray](https://leetcode.cn/problems/maximum-sum-circular-subarray/)

Given a **circular integer array** `nums` of length `n`, return *the maximum possible sum of a non-empty **subarray** of* `nums`.

A **circular array** means the end of the array connects to the beginning of the array. Formally, the next element of `nums[i]` is `nums[(i + 1) % n]` and the previous element of `nums[i]` is `nums[(i - 1 + n) % n]`.

A **subarray** may only include each element of the fixed buffer `nums` at most once. Formally, for a subarray `nums[i], nums[i + 1], ..., nums[j]`, there does not exist `i <= k1`, `k2 <= j` with `k1 % n == k2 % n`.

> **Example 1:**
>
> ```
> Input: nums = [1,-2,3,-2]
> Output: 3
> Explanation: Subarray [3] has maximum sum 3.
> ```
>
> **Example 2:**
>
> ```
> Input: nums = [5,-3,5]
> Output: 10
> Explanation: Subarray [5,5] has maximum sum 5 + 5 = 10.
> ```
>
> **Example 3:**
>
> ```
> Input: nums = [-3,-2,-3]
> Output: -2
> Explanation: Subarray [-2] has maximum sum -2.
> ```

## Solution Approach

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubarraySumCircular = function(nums) {
    // Helper function: Use Kadane's Algorithm to find the maximal sum of a non-circular subarray.
    const kadane = (arr) => {
        let maxEndingHere = arr[0];
        let maxSoFar = arr[0];
        for (let i = 1; i < arr.length; i++) {
            maxEndingHere = Math.max(arr[i], maxEndingHere + arr[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
    };

    // STEP1：Find the maximal sum of a non-circular subarray.
    const maxKadane = kadane(nums);

    // STEP2：Find the maximal sum of a circular subarray.
    const totalSum = nums.reduce((a, b) => a + b, 0); // The sum of all elements in `nums`.
    const maxWrap = totalSum + kadane(nums.map(num => -num)); // Subtract the sum of the minimal subarray from the total sum of the array.

    // Special case: If maxWrap is 0, it means the array is full of negative values. In this case, the sum of the maximal subarray should be maxKadane.
    if (maxWrap === 0) return maxKadane;

    // Return the larger one between the two.
    return Math.max(maxKadane, maxWrap);
};

// 示例调用
console.log(maxSubarraySumCircular([1, -2, 3, -2])); // 输出：3
console.log(maxSubarraySumCircular([5, -3, 5])); // 输出：10
console.log(maxSubarraySumCircular([3, -2, 2, -3])); // 输出：3
console.log(maxSubarraySumCircular([-3, -2, -3])); // 输出：-2
```

