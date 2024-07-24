# [Rotate Array](https://leetcode.cn/problems/rotate-array/)

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

 

**Example 1:**

```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

**Example 2:**

```
Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

 ```js
 /**
  * @param {number[]} nums
  * @param {number} k
  * @return {void} Do not return anything, modify nums in-place instead.
  */
 var rotate = function(nums, k) {
     
  }
 ```

**Constraints:**

- `1 <= nums.length <= 105`
- `-231 <= nums[i] <= 231 - 1`
- `0 <= k <= 105`

**Follow up:**

- Try to come up with as many solutions as you can. There are at least **three** different ways to solve this problem.
- Could you do it in-place with `O(1)` extra space?

## Solution Approach

Suppose the length of the array `nums` is `n` and the rotation count is `k`. First, we take `k` modulo `n` to ensure `k` does not exceed `n`.

```js
k = k % n;
```

Next, we will perform three reversals:

1. Reverse the entire array.
2. Reverse the first k elements.
3. Reverse the elements from position `k` to the end.

## Full Code

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var rotate = function(nums, k) {
    // get the array length
    const n = nums.length;
    
    // If the array length is either 0 or 1, return it directly without performing any rotations.
    if (n <= 1) return;
    
    // Calculate the valid steps
    k = k % n;
    
    //  Define a function to reverse an array
    const reverse = (arr, start, end) => {
        while (start < end) {
            [arr[start], arr[end]] = [arr[end], arr[start]];
            start++;
            end--;
        }
    };
    
    // step1: reverse the entire array
    reverse(nums, 0, n - 1);
    // step2: reverse the first k elements
    reverse(nums, 0, k - 1);
    // step3: reverse the rest elements
    reverse(nums, k, n - 1);
};
```



