# [Minimum Size Subarray Sum](https://leetcode.cn/problems/minimum-size-subarray-sum/)

Given an array of positive integers `nums` and a positive integer `target`, return *the **minimal length** of a* *subarray* *whose sum is greater than or equal to* `target`. If there is no such subarray, return `0` instead.



**Example 1:**

```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```

**Example 2:**

```
Input: target = 4, nums = [1,4,4]
Output: 1
```

**Example 3:**

```
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```

 ## Solution Approach

```js
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function(target, nums) {
    // The `left` pointer starts from the begining of `nums`.
    let left = 0;
    // Initialize sum to 0; it is used to store the sum of elements in the current window.
    let sum = 0;
    // Initialize minLength to Infinity; it is used to record the minimum subarray length.
    let minLength = Infinity;

    for (let right = 0; right < nums.length; right++) {
        // Traverse nums, moving right and adding nums[right] to sum each time.
        sum += nums[right];

        while (sum >= target) {
            // When sum is greater than or equal to target, record the length of the current window.
            minLength = Math.min(minLength, right - left + 1);
            // Move left to narrow the window until sum is less than target.
            sum -= nums[left];
            left++;
        }
    }
	
    return minLength === Infinity ? 0 : minLength;
};

// 示例调用
console.log(minSubArrayLen(7, [2,3,1,2,4,3])); // 输出：2
console.log(minSubArrayLen(4, [1,4,4]));       // 输出：1
console.log(minSubArrayLen(11, [1,1,1,1,1,1,1,1])); // 输出：0
```

