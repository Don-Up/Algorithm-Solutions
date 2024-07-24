# [Path Sum](https://leetcode.cn/problems/path-sum/)

Given the `root` of a binary tree and an integer `targetSum`, return `true` if the tree has a **root-to-leaf** path such that adding up all the values along the path equals `targetSum`.

A **leaf** is a node with no children.

> **Example 1:**
>
> <img src="https://assets.leetcode.com/uploads/2021/01/18/pathsum1.jpg" alt="img" style="zoom:50%;" />
>
> ```
> Input: root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
> Output: true
> Explanation: The root-to-leaf path with the target sum is shown.
> ```
>
> **Example 2:**
>
> ![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)
>
> ```
> Input: root = [1,2,3], targetSum = 5
> Output: false
> Explanation: There two root-to-leaf paths in the tree:
> (1 --> 2): The sum is 3.
> (1 --> 3): The sum is 4.
> There is no root-to-leaf path with sum = 5.
> ```
>
> **Example 3:**
>
> ```
> Input: root = [], targetSum = 0
> Output: false
> Explanation: Since the tree is empty, there are no root-to-leaf paths.
> ```

## Solution Approach

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} targetSum
 * @return {boolean}
 */
var hasPathSum = function(root, targetSum) {
    if (root === null) {
        return false;
    }
    
    function next(node, sum) {
        // Calculate the sum of the current path.
        sum += node.val;
        
        // Determine if node is a leaf node.
        if (node.left === null && node.right === null) {
            // If sum equals targetSum, it means the desired path exists.
            return sum === targetSum;
        }
        
        // Recursively check the left and right subtrees.
        if (node.left !== null && next(node.left, sum)) {
            return true;
        }
        if (node.right !== null && next(node.right, sum)) {
            return true;
        }
        
        // Return false by default.
        return false;
    }
    
    // Start the recursion.
    return next(root, 0);
};

```

