# [Contains Duplicate II](https://leetcode.cn/problems/contains-duplicate-ii/)

Given an integer array `nums` and an integer `k`, return `true` *if there are two **distinct indices*** `i` *and* `j` *in the array such that* `nums[i] == nums[j]` *and* `abs(i - j) <= k`.

> **Example 1:**
>
> ```
> Input: nums = [1,2,3,1], k = 3
> Output: true
> ```
>
> **Example 2:**
>
> ```
> Input: nums = [1,0,1,1], k = 1
> Output: true
> ```
>
> **Example 3:**
>
> ```
> Input: nums = [1,2,3,1,2,3], k = 2
> Output: false
> ```

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {boolean}
 */
const containsNearbyDuplicate = function(nums, k) {
    let table = new Map()
    for (let i = 0; i < nums.length; i++) {
       if(!table.has(nums[i])) {
           // Record the position of the latest occurrence of the number.
           table.set(nums[i], i)
       } else {
           // If the number already exists in the table, compare the current position to the position of its last occurrence.
           if(Math.abs(i-table.get(nums[i]))<=k) {
               return true
           } else {
               // If the distance between the two positions exceeds k, update the number's position to the current position.
               table.set(nums[i], i)
           }
       }
    }
    return false
};
```

