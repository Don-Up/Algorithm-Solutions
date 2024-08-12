# find corresponding node in two identical DOM tree

Given two same DOM tree **A**, **B**, and an Element **a** in **A**, find the corresponding Element **b** in **B**.

By **corresponding**, we mean **a** and **b** have the same relative position to their DOM tree root.

*follow up*

This could be a problem on general Tree structure with only `children`.

Could you solve it recursively and iteratively?

Could you solve this problem with special DOM api for better performance?

What are the time cost for each solution?

## Solution Approach

To solve the problem of finding the corresponding node in a cloned DOM tree, we need to ensure that we traverse both trees in a synchronized manner. This ensures that we are always comparing nodes in the same relative positions.

### Recursive Solution

The recursive approach involves traversing the tree from the root and checking if the current node in tree A matches the target node. If it does, we return the corresponding node from tree B. If not, we recursively check the children.

Here is the implementation:

```js

/**
 * @param {HTMLElement} rootA
 * @param {HTMLElement} rootB - rootA and rootB are clone of each other
 * @param {HTMLElement} nodeA
 */
const findCorrespondingNode = (rootA, rootB, nodeA) => {
  if (rootA === nodeA) {
    return rootB;
  }

  // Iterate over each child of rootA
  for (let i = 0; i < rootA.children.length; i++) {
    // Recursively call findCorrespondingNode until finding the corresponding rootB.
    const result = findCorrespondingNode(
        rootA.children[i], 
        rootB.children[i], 
        nodeA
    );
    if (result) {
      // If result is founded, we return it.
      return result;
    }
  }

  return null;
};
```

### Iterative Solution

The iterative solution uses a breadth-first traversal (BFS) approach to synchronize the traversal of both trees. This is done using two queues to keep track of the current nodes in both trees.

Here is the implementation:

```js
/**
 * @param {HTMLElement} rootA
 * @param {HTMLElement} rootB - rootA and rootB are clone of each other
 * @param {HTMLElement} nodeA
 * @return {HTMLElement}
 */
const findCorrespondingNodeIterative = (rootA, rootB, nodeA) => {
  const queueA = [rootA];
  const queueB = [rootB];

  while (queueA.length > 0) {
    const currentNodeA = queueA.shift();
    const currentNodeB = queueB.shift();

    if (currentNodeA === nodeA) {
      return currentNodeB;
    }

    for (let i = 0; i < currentNodeA.children.length; i++) {
      queueA.push(currentNodeA.children[i]);
      queueB.push(currentNodeB.children[i]);
    }
  }

  return null;
};
```

### Special DOM API

If the problem is specific to the DOM and involves a cloned tree, we can make use of the `Node` interface's `compareDocumentPosition` method. This method can help us determine the position of nodes relative to each other.

However, using this method directly for finding the corresponding node might not be straightforward. The traversal methods described above are more direct and easier to understand.

### Time Complexity

For both recursive and iterative solutions, the time complexity is O(n), where n is the number of nodes in the tree. This is because, in the worst case, we might need to traverse all nodes in the tree to find the corresponding node.

### Summary

- **Recursive Solution:** Traverses the tree synchronously in a depth-first manner.
- **Iterative Solution:** Traverses the tree synchronously in a breadth-first manner.
- **Time Complexity:** O(n) for both solutions, where n is the number of nodes in the tree.

These solutions ensure that we can accurately find the corresponding node in the cloned DOM tree efficiently.