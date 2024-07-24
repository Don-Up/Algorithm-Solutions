# [Longest Consecutive Sequence](https://leetcode.cn/problems/longest-consecutive-sequence/)

Given an unsorted array of integers `nums`, return *the length of the longest consecutive elements sequence.*

You must write an algorithm that runs in `O(n)` time.

>  **Example 1:**
>
> ```
> Input: nums = [100,4,200,1,3,2]
> Output: 4
> Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
> ```
>
> **Example 2:**
>
> ```
> Input: nums = [0,3,7,2,5,8,4,6,0,1]
> Output: 9
> ```

## Solution Approach

To find the longest consecutive sequence of an unsorted array :

1. We should use a set to wrap the array for efficient searching and duplicate element elimination.
2. Next, start a `for...of` loop on `numSet`. For each `num`, check if it is the beginning of a certain sequence. If not, continue to the next iteration. If it is, recursively auto-increment a copy of `num` until it no longer exists in `numSet`. This way, you can determine the length of the sequence that starts with `num`.
3. Finally, update `maxLength` as needed until the loop is over and then return it.


```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var longestConsecutive = function(nums) {
    if (nums.length === 0) {
        return 0;
    }
	
    // Use a Set to wrap nums, removing duplicate elements.
    const numSet = new Set(nums);
    // Declare a maxLength to record the length of the longest consecutive sequence.
    let maxLength = 0;

    for (let num of numSet) {
        // If num-1 doesn't exist in numSet, it means num is the beginning of a certain sequence.
        if (!numSet.has(num - 1)) {
            let currentNum = num;
			
            // Auto-increment currentNum until numSet no longer contains currentNum.
            while (numSet.has(currentNum + 1)) {
                currentNum++;
            }
		   
            // Compare the original maxLength with current-num+1 to update maxLength.
            maxLength = Math.max(maxLength, currentNum-num+1);
        }
    }

    return maxLength;
};
```

