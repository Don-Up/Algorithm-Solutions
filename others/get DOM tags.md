#  get DOM tags

Given a DOM tree, please return all the tag names it has.

Your function should return a unique array of tags names in lowercase, order doesn't matter.

## Solution Approach

Key points: 

1. Element.nodeType
2. Element.childNodes
3. Element.tagName

```js

/**
 * @param {HTMLElement} tree
 * @return {string[]}
 */
function getTags(tree) {
  const tags = new Set()

  function traverse(node){
    if(node.nodeType === Node.ELEMENT_NODE){
      // Add the tag name of the current node to the set in lowercase
      tags.add(node.tagName.toLowerCase())
      // Recursively traverse child nodes
      node.childNodes.forEach(child => {
        traverse(child)
      })
    }
  }
  
  traverse(tree)
    
  // Convert the set to an array and return it
  return [...tags]
}
```

