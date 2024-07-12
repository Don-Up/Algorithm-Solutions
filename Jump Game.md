# Jump Game

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` *if you can reach the last index, or* `false` *otherwise*.

 

**Example 1:**

```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**

```
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
```

 ```js
 /**
  * @param {number[]} nums
  * @return {boolean}
  */
 var canJump = function(nums) {
     
 }
 ```

**Constraints:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 105`

## Solution Approach

We need to declare a variable `maxIndex` to record the farthest reachable position for each number.

We iterate over the `nums`. If `maxIndex` is less than the current index, it means the current position is not reachable, and we can return `false`. Otherwise, we update `maxIndex` by calling `Math.max` with `maxIndex` and `i + nums[i]`. When `maxIndex` is updated, determine if `maxIndex` is greater than or equal to `nums.length - 1`. If the condition is true, we can directly return `true`.

## Full Code

```js
var canJump = function(nums) {
    // Declare a variable to record the farthest position that can be reached from the current element
    let maxIndex = 0;

    for (let i = 0; i < nums.length; i++) {
        // If maxIndex is already less than the current index, it means the current position is not reachable, return false
        if (i > maxIndex) {
            return false;
        }
        // If it is reachable, update the maxIndex for the current index
        maxIndex = Math.max(maxIndex, i + nums[i]);
        // If the current maxIndex can already reach the last position, return true directly
        if (maxIndex >= nums.length - 1) {
            return true;
        }
    }
};
```

