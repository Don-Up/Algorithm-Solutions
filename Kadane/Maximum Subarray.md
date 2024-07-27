# [Maximum Subarray](https://leetcode.cn/problems/maximum-subarray/)

Given an integer array `nums`, find the subarray with the largest sum, and return *its sum*.

> **Example 1:**
>
> ```
> Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
> Output: 6
> Explanation: The subarray [4,-1,2,1] has the largest sum 6.
> ```
>
> **Example 2:**
>
> ```
> Input: nums = [1]
> Output: 1
> Explanation: The subarray [1] has the largest sum 1.
> ```
>
> **Example 3:**
>
> ```
> Input: nums = [5,4,-1,7,8]
> Output: 23
> Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.
> ```

## Solution Approach

To find the continuous subarray with the maximal sum, we can use **Kadane's Algorithm**, which can solve the problem with a time complexity of O(n).

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    // To record the sum of the current subarray.
    let currentSum = nums[0]
    // To record the sum of the maximal subarray.
    let maxSum = nums[0]
    
    // Traverse `nums` starting from the second element.
    for(let i=1; i<nums.length; i++){
        // Update `currentSum` to the higher value between the current element and the sum of the current element and the previous `currentSum`.
        // It means if the previous `currentSum` is negative, recalculate `currentSum`.
        currentSum = Math.max(nums[i], currentSum + nums[i])
        // Update the higher value between `maxSum` and `currentSum `.
        maxSum = Math.max(maxSum, currentSum)
    }
    
    return maxSum
}
```

> ```
> [-2,1,-3,4,-1,2,1,-5,4]
> currentSum = -2
> maxSum = - 2
> 
> i = 1
> currentSum = Math.max(nums[i] (1), currentSum (-2) + nums[i] (1))
>            = Math.max(1, -1)
>            = 1
> maxSum = Math.max(maxSum (-2), currentSum (1))
>        = Math.max(-2, 1)
>        = 1
> 
> i = 2
> currentSum = Math.max(nums[i] (-3), currentSum (1) + nums[i] (-3))
>            = Math.max(-3, -2)
>            = -2
> maxSum = Math.max(maxSum (1), currentSum (-2))
>        = Math.max(1, -2)
>        = 1
> 
> i = 3
> currentSum = Math.max(nums[i] (4), currentSum (-2) + nums[i] (4))
>            = Math.max(4, 2)
>            = 4
> maxSum = Math.max(maxSum (1), currentSum (4))
>        = Math.max(1, 4)
>        = 4
> 
> i = 4
> currentSum = Math.max(nums[i] (-1), currentSum (4) + nums[i] (-1))
>            = Math.max(-1, 3)
>            = 3
> maxSum = Math.max(maxSum (4), currentSum (3))
>        = Math.max(4, 3)
>        = 4
> 
> i = 5
> currentSum = Math.max(nums[i] (2), currentSum (3) + nums[i] (2))
>            = Math.max(2, 5)
>            = 5
> maxSum = Math.max(maxSum (4), currentSum (5))
>        = Math.max(4, 5)
>        = 5
> 
> i = 6
> currentSum = Math.max(nums[i] (1), currentSum (5) + nums[i] (1))
>            = Math.max(1, 6)
>            = 6
> maxSum = Math.max(maxSum (5), currentSum (6))
>        = Math.max(5, 6)
>        = 6
> 
> i = 7
> currentSum = Math.max(nums[i] (-5), currentSum (6) + nums[i] (-5))
>            = Math.max(-5, 1)
>            = 1
> maxSum = Math.max(maxSum (6), currentSum (1))
>        = Math.max(6, 1)
>        = 6
> 
> i = 8
> currentSum = Math.max(nums[i] (4), currentSum (1) + nums[i] (4))
>            = Math.max(4, 5)
>            = 5
> maxSum = Math.max(maxSum (6), currentSum (5))
>        = Math.max(6, 5)
>        = 6
> ```



