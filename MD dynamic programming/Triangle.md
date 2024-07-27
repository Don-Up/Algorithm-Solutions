# [Triangle](https://leetcode.cn/problems/triangle/)

Given a `triangle` array, return *the minimum path sum from top to bottom*.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

> **Example 1:**
>
> ```
> Input: triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
> Output: 11
> Explanation: The triangle looks like:
>    2
>   3 4
>  6 5 7
> 4 1 8 3
> The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).
> ```
>
> **Example 2:**
>
> ```
> Input: triangle = [[-10]]
> Output: -10
> ```

## Solution Approach

1. Perform dynamic programming from bottom to top.
2. For each element, choose the smaller value between the two adjacent elements of the row below, add the current element's value, and update the current element's value.
3. Finally, the sum of the minimum path will be located at the top of the triangle.

```js
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function(triangle) {
    // Start from the 2nd level from the bottom and handle each level upward.
    for (let row = triangle.length - 2; row >= 0; row--) {
        for (let col = 0; col < triangle[row].length; col++) {
            // For each element of each level, calculate the minimum sum of it and the two adjacent elements of the level below, and update it to the new value of the current element.
            triangle[row][col] += Math.min(triangle[row + 1][col], triangle[row + 1][col + 1]);
        }
    }
    // Return the top element's value, which is the minimum path sum.
    return triangle[0][0];
};
```

