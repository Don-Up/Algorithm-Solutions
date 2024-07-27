# [Sum Root to Leaf Numbers](https://leetcode.cn/problems/sum-root-to-leaf-numbers/)

You are given the `root` of a binary tree containing digits from `0` to `9` only.

Each root-to-leaf path in the tree represents a number.

- For example, the root-to-leaf path `1 -> 2 -> 3` represents the number `123`.

Return *the total sum of all root-to-leaf numbers*. Test cases are generated so that the answer will fit in a **32-bit** integer.

A **leaf** node is a node with no children.

## Solution Approach

To calculate the sum of numbers represented by all root-to-leaf paths, we can use Depth-First Search (DFS). While traversing each path, we maintain the current path's sum by accumulating the value of the current node into the sum.

### Steps

1. Define a recursive function `dfs(node, currentSum)` where `node` represents the current node and `currentSum` represents the sum formed by the path from the root node to the current node.
2. If the current node is empty, return 0.
3. Update `currentSum` to `currentSum * 10 + node.val`.
4. If the current node is a leaf node (i.e., it has no left or right child nodes), return `currentSum`.
5. Recursively calculate the path's sum for the left and right subtrees, add them together, and return the result.

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
 * @return {number}
 */
var sumNumbers = function(root) {
    // Define the recursive function for DFS
    function dfs(node, currentSum) {
        // If the current node is empty, return 0
        if (node === null) {
            return 0;
        }

        // Update currentSum
        currentSum = currentSum * 10 + node.val;

        // If the current node is a leaf node, return currentSum
        if (node.left === null && node.right === null) {
            return currentSum;
        }

        // Recursively calculate the path's sum for left and right subtrees
        return dfs(node.left, currentSum) + dfs(node.right, currentSum);
    }

    // Start the DFS from the root with an initial sum of 0
    return dfs(root, 0);
};
```

