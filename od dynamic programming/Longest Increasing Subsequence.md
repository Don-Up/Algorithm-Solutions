# [Longest Increasing Subsequence](https://leetcode.cn/problems/longest-increasing-subsequence/)

Given an integer array `nums`, return *the length of the longest **strictly increasing subsequence***.

**Example 1:**

```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```

**Example 2:**

```
Input: nums = [0,1,0,3,2,3]
Output: 4
```

**Example 3:**

```
Input: nums = [7,7,7,7,7,7,7]
Output: 1
```

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var lengthOfLIS = function(nums) {

};
```

## Solution Approach

To solve the problem of the longest increasing subsequence (LIS), we can use dynamic programming or a greedy algorithm with binary search.

### Approach 1: Dynamic programming

Dynamic programming is a classical way to solve the LIS problem, with a time complexity of O(n^2).

#### Initialization

* Create an array `dp`, where`dp[i]` indicates the length of the longest increasing subsequence ending with `num[i]`. Initialize all elements of `dp` to 1, because every element can independently form a subsequence.

#### * State Translation

For each `i` from 0 to `nums.length - 1`, traverse `j` from 0 to `i - 1`. If `nums[i] > nums[j]`, update `dp[i]` to `Math.max(dp[i], dp[j] + 1)`.

#### Result

* Finally, return the maximum value in `dp`, which represents the length of the LIS.

```js
var lengthOfLIS = function(nums) {
    if (nums.length === 0) return 0;
    let dp = new Array(nums.length).fill(1);
    for (let i = 1; i < nums.length; i++) {
        for (let j = 0; j < i; j++) {
            if (nums[i] > nums[j]) {
                dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }
    }
    return Math.max(...dp);
};
```

### Approach 2: Greedy Algorithm + Binary Search

Using a greedy algorithm with binary search can reduce the time complexity to O(n log n).

#### maintain an array

* Create an array `tails`, where `tails[i]` indicates the minimum value of the last element of all increasing subsequences of length `i + 1`.

#### Iterate over the array

* For each element in `nums`, use binary search to find the first position in `tails` that is greater than or equal to it, update `tails`. If such an element can't be found, append it to the end of  `tails`.

#### Result

Finally, the length of `tails` represents the length of the LIS.

```js
var lengthOfLIS = function(nums) {
    let tails = [];
    for (let num of nums) {
        let left = 0, right = tails.length;
        while (left < right) {
            let mid = Math.floor((left + right) / 2);
            if (tails[mid] < num) left = mid + 1;
            else right = mid;
        }
        if (right >= tails.length) tails.push(num);
        else tails[right] = num;
    }
    return tails.length;
}
```







