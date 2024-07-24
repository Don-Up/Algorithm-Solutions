# [Summary Ranges](https://leetcode.cn/problems/summary-ranges/)

You are given a **sorted unique** integer array `nums`.

A **range** `[a,b]` is the set of all integers from `a` to `b` (inclusive).

Return *the **smallest sorted** list of ranges that **cover all the numbers in the array exactly***. That is, each element of `nums` is covered by exactly one of the ranges, and there is no integer `x` such that `x` is in one of the ranges but not in `nums`.

Each range `[a,b]` in the list should be output as:

- `"a->b"` if `a != b`
- `"a"` if `a == b`

> **Example 1:**
>
> ```
> Input: nums = [0,1,2,4,5,7]
> Output: ["0->2","4->5","7"]
> Explanation: The ranges are:
> [0,2] --> "0->2"
> [4,5] --> "4->5"
> [7,7] --> "7"
> ```
>
> **Example 2:**
>
> ```
> Input: nums = [0,2,3,4,6,8,9]
> Output: ["0","2->4","6","8->9"]
> Explanation: The ranges are:
> [0,0] --> "0"
> [2,4] --> "2->4"
> [6,6] --> "6"
> [8,9] --> "8->9"
> ```

```js
/**
 * @param {number[]} nums
 * @return {string[]}
 */
var summaryRanges = function(nums) {
    // Define a result array to collect the ranges. 
    const result = []
    // Define start and end to record the current range.
    let start = 0
    let end = 0

    for (let i = 0; i < nums.length; i++) {
        // A new range needs to be collected when either of the following conditions occurs:
        // 1. The current sequence is interrupted (nums[i+1]-nums[i] !== 1).
        // 2. Reaching the end of the array (i === nums.length - 1).
        if(nums[i+1]-nums[i] !== 1 || i === nums.length-1){
            // Push nums[i] or ${nums[start]}->${nums[i]} into result based on whether start equals i.
            result.push(start===i?`${nums[i]}`:`${nums[start]}->${nums[i]}`)
            // Update both start and end by setting them to i+1 to record the next range.
            start = i+1
            end = i+1
        }
    }
    
    return result
}
```

