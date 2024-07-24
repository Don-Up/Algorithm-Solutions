# [3Sum](https://leetcode.cn/problems/3sum/)

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

 

**Example 1:**

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
```

**Example 2:**

```
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
```

**Example 3:**

```
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
```

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {

};
```

## Solution Approach

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
    const results = [];
    // If the length of nums is less than 3, we can directly return results.
    if (nums.length < 3) return results;

    // Sort `nums` in ascending order.
    nums.sort((a, b) => a - b);

    for (let i = 0; i < nums.length - 2; i++) {
        // If the current num is greater than 0, the subsequent numbers will also be greater than 0, making it impossible to find triplets that sum to 0.
        if (nums[i] > 0) break;

        // Skip duplicate elements.
        if (i > 0 && nums[i] === nums[i - 1]) continue;
		
        // Initialize the `left` pointer to `i` plus 1.
        // Initialize the `right` pointer to `num.length` minus 1.
        let left = i + 1;
        let right = nums.length - 1;
		
        // Continue the while loop as long as left is less than right.
        while (left < right) {
            // Sum up num[i], nums[left], and nums[right] into sum.
            const sum = nums[i] + nums[left] + nums[right];
            if (sum === 0) {
                // If sum is equal to 0, push the array consisting of nums[i], nums[left], and nums[right] into results.
                results.push([nums[i], nums[left], nums[right]]);
                // Skip duplicate elements.
                while (left < right && nums[left] === nums[left + 1]) left++;
                while (left < right && nums[right] === nums[right - 1]) right--;
                // Move the left and right pointers.
                left++;
                right--;
            } else if (sum < 0) {
                // If sum is less than 0, it means left is too small, so move it to the right.
                left++;
            } else {
                // If sum is greater than 0, it means right is too large, so move it to the left.
                right--;
            }
        }
    }

    return results;
};

// 示例调用
console.log(threeSum([-1, 0, 1, 2, -1, -4])); // 输出：[[-1,-1,2],[-1,0,1]]
console.log(threeSum([0, 1, 1]));             // 输出：[]
console.log(threeSum([0, 0, 0]));             // 输出：[[0,0,0]]
```

