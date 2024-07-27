# [Search Insert Position](https://leetcode.cn/problems/search-insert-position/)

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

> **Example 1:**
>
> ```
> Input: nums = [1,3,5,6], target = 5
> Output: 2
> ```
>
> **Example 2:**
>
> ```
> Input: nums = [1,3,5,6], target = 2
> Output: 1
> ```
>
> **Example 3:**
>
> ```
> Input: nums = [1,3,5,6], target = 7
> Output: 4
> ```

## Solution Approach

To find the target value's position in a sorted array, and if the target value is non-existent, return the position where it should be inserted, you can use the binary search algorithm. The time complexity of binary search is O(log n), making it very suitable for this problem.

## Steps

Your explanation is mostly clear but can be slightly refined for better readability and clarity:

1. Initialize pointers `left` and `right`, which point to the beginning and end of the array respectively.
2. Perform a binary search to calculate the middle position `mid`.
3. Compare `nums[mid]` with `target`:
   1. If they are equal, return `mid`.
   2. If `nums[mid]` is less than `target`, update `left` to `mid + 1`.
   3. If `nums[mid]` is greater than `target`, update `right` to `mid - 1`.
4. When `left` surpasses `right`, return `left`. At this moment, `left` is the position where `target` should be inserted.

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
    // 1. Pointer Initialization
    
    // `left` points to the beginning
    let left = 0;
    // `right` points to the end
    let right = nums.length - 1;
    
    // 2. Binary Search
    
    while (left <= right) {
        // Calculate the middle position `mid`.
        const mid = Math.floor((left + right) / 2);
        
        // Compare `nums[mid]` with target and execute different actions.
        if (nums[mid] === target) {
            // Return `mid` if the target is found.
            return mid;
        } else if (nums[mid] < target) {
            // Narrow the left range.
            left = mid + 1;
        } else {
            // Narrow the right range.
            right = mid - 1;
        }
    }
    
    // If the target is not found, return the position where it should be inserted.
    return left;
};
```

