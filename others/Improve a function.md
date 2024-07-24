#  Improve a function

```js
// Given an input of array, 
// which is made of items with >= 3 properties
let items = [
  {color: 'red', type: 'tv', age: 18}, 
  {color: 'silver', type: 'phone', age: 20},
  {color: 'blue', type: 'book', age: 17}
] 
// an exclude array made of key value pair
const excludes = [ 
  {k: 'color', v: 'silver'}, 
  {k: 'type', v: 'tv'}, 
  ...
] 
function excludeItems(items, excludes) { 
  excludes.forEach( pair => { 
    items = items.filter(item => item[pair.k] === item[pair.v])
  })
 
  return items
} 
```

1. What does this function `excludeItems` do?
2. Is this function working as expected ?
3. What is the time complexity of this function?
4. How would you optimize it ?

*note*

we only judge by the result, not the time cost. please submit the best approach you can.

## Soltion Approach

### Analysis:

1. **Function Purpose**:
   The `excludeItems` function is intended to filter out items from an array based on an exclude array. Each exclude array entry has a key (`k`) and a value (`v`), and the function should exclude items that have a matching key-value pair.

2. **Function Behavior**:
   The current implementation of `excludeItems` is not working as expected. It should exclude items that match any of the key-value pairs in the `excludes` array, but the current implementation is keeping items that match the criteria instead of excluding them.

3. **Time Complexity**:
   The time complexity of the current implementation is \(O(n \times m)\), where \(n\) is the number of items in the `items` array and \(m\) is the number of exclude pairs. This is because it performs a filter operation for each exclude pair, iterating over the items array each time.

4. **Optimization**:
   The optimized approach should correctly exclude items that match any of the key-value pairs and do so efficiently.

### Optimized Solution:

To optimize and correct the function:

1. Use a single filter operation.
2. Check for each item if it matches any of the exclude criteria.

Here is the optimized implementation:

```javascript
/**
 * @param {object[]} items
 * @param { Array<{k: string, v: any}> } excludes
 * @return {object[]}
 */
function excludeItems(items, excludes) {
  // Convert the exclude array to a set of conditions for faster lookups
  const excludeSet = new Set(excludes.map(({ k, v }) => `${k}:${v}`));

  // Filter items that do not match any of the exclude conditions
  return items.filter(item => {
    return !excludes.some(pair => item[pair.k] === pair.v);
  });
}

// Example usage:
let items = [
  {color: 'red', type: 'tv', age: 18}, 
  {color: 'silver', type: 'phone', age: 20},
  {color: 'blue', type: 'book', age: 17}
]; 

const excludes = [ 
  {k: 'color', v: 'silver'}, 
  {k: 'type', v: 'tv'}
]; 

console.log(excludeItems(items, excludes));
// Output should be: [ {color: 'blue', type: 'book', age: 17} ]
```

### Explanation of the Optimized Function:

1. **Convert Excludes to a Set**:
   - Create a set from the excludes array to enable faster lookups. This step is optional but demonstrates a common optimization pattern.

2. **Filter Items**:
   - Use a single filter operation to check each item.
   - For each item, use the `some` method to determine if any of the exclude conditions are met.
   - If an item matches any exclude condition, it is excluded from the result.

This approach ensures that we filter the items array in a single pass, making it more efficient and straightforward. The resulting time complexity is still \(O(n \times m)\), but the logic is clear and correct.