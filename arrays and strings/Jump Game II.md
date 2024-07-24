# Jump Game II

You are given a **0-indexed** array of integers `nums` of length `n`. You are initially positioned at `nums[0]`.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`. In other words, if you are at `nums[i]`, you can jump to any `nums[i + j]` where:

- `0 <= j <= nums[i]` and
- `i + j < n`

Return *the minimum number of jumps to reach* `nums[n - 1]`. The test cases are generated such that you can reach `nums[n - 1]`.

 

**Example 1:**

```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**

```
Input: nums = [2,3,0,1,4]
Output: 2
```

 ```js
 /**
  * @param {number[]} nums
  * @return {number}
  */
 var jump = function (nums) {
     
 }
 ```

**Constraints:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 1000`
- It's guaranteed that you can reach `nums[n - 1]`.

## Solution Approach

To solve the "Jump Game II" problem, we can use a greedy algorithm to determine the minimum number of jumps required to reach the last index. The main idea is to keep track of the farthest point that can be reached with the current number of jumps and to increment the jump count only when we reach the end of the current farthest point.

Here's a step-by-step breakdown of the algorithm:

#### Initialize Virables:

* `jumps` to count the number of jumps needed.
* `current_end` to keep track of the end of the range that can be reached with the current number of jumps.
* `farthest` to keep track of the farthest point that can be reached with the next jump.

#### Iterate through the array

* For each index `i`, update the `farthest` point that can reached from the current index.
* If `i` reaches `current_end`, increment the jump count and update `current_end` to `farthest`. This means we have used one more jump and now the new range to consider for the next jump is up to `farthest`.

#### End Condition

* The loop will end when `current_end` reaches or exceeds the last index of the array. At this point,  `jumps` will contain the mininum number of jumps needed to reach the end.

The greedy approach works efficiently here because it ensures that we make the optimal jump at each step by always considering the farthest point we can reach.

## Full Code

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var jump = function(nums) {
    let jumps = 0;
    let current_end = 0;
    let farthest = 0;
    
    for (let i = 0; i < nums.length - 1; i++) {
        // Update the farthest point that can be reached
        farthest = Math.max(farthest, i + nums[i]);
        
        // If we have reached the end of the current jump range
        if (i === current_end) {
            jumps++;
            current_end = farthest;
            
            // Early exit if we can already reach the end
            if (current_end >= nums.length - 1) {
                break;
            }
        }
    }
    
    return jumps;
};
```

