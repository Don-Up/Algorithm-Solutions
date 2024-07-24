# [House Robber](https://leetcode.cn/problems/house-robber/)

![image-20240720102614398](assets/image-20240720102614398.png)

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return *the maximum amount of money you can rob tonight **without alerting the police***.

 

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.
```

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function(nums) {

};
```

## Solution Approach

To solve the House Robber problem, you can use dynamic programming. The key idea is to determine the maximum amount of money that can be robbed up to each house without robbing two adjacent houses.

### Base Case:

* If there are no houses, the maximum amount of money is 0.
* If there is only one house, the maximum amount of money is the amount in that house.

### Recursive Relation:

* For each house `i`, you have two options:
  * Do not rob the current house, in which case the maximum of money is the same as the maximum amount up to the previous house(`dp[i-1]`) .
  * Rob the current house, in which case you add the money in the current house to the maximum amount of money up to the house before the previous house(`nums[i]+dp[i-2]`)
  * The formula becomes: `dp[i] = Math.max(dp[i-1], nums[i]+(dp[i-2] || 0))`

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function(nums) {
    if(nums.length === 0) return 0
    if(nums.length === 1) return nums[0]
    
    let dp = new Array(nums.length)
    // the maximum money for the first house is the money in the first house
    dp[0] = nums[0]
    // the maximum money for the second house is the maximum of the first two houses
    dp[1] = Math.max(nums[0], nums[1])
    
    // for each house from the third to the last, calculate the maximum money by considering whether to rob the current house or not.
    for(let i=2; i < nums.length; i++){
        dp[i] = Math.max(dp[i-1], nums[i]+dp[i-2])
    }
    
    // give the maximum amount of money that can be robbed without alerting the police
    return dp[nums.length-1]
}
```

### Space Optimization

Since you only need the last two values of the `dp` array at any time, you can optimize the space complexity to O(1) by using two variables instead of an array.

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function(nums) {
    if(nums.length === 0) return 0
    if(nums.length === 1) return nums[0]
    
    let prev1 = nums[0]
    let prev2 = Math.max(nums[0], nums[1])
    
    for(let i = 2; i < nums.length; i++){
        let current = Math.max(prev2, nums[i]+prev1)
        prev1 = prev2
        prev2 = current
    }
    
    return prev2
}
```

In this optimized version, `prev1` and `prev2` are used to store the maximum money that can be robbed up to previous two houses, and `current` is used to store the maximum money for the current house. This reduces the space complexity from 0(n) to 0(1).
