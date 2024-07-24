# [Insert Delete GetRandom O(1)](https://leetcode.cn/problems/insert-delete-getrandom-o1/)

Implement the `RandomizedSet` class:

- `RandomizedSet()` Initializes the `RandomizedSet` object.
- `bool insert(int val)` Inserts an item `val` into the set if not present. Returns `true` if the item was not present, `false` otherwise.
- `bool remove(int val)` Removes an item `val` from the set if present. Returns `true` if the item was present, `false` otherwise.
- `int getRandom()` Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the **same probability** of being returned.

You must implement the functions of the class such that each function works in **average** `O(1)` time complexity.

 

**Example 1:**

```
Input
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
Output
[null, true, false, true, 2, true, false, 2]

Explanation
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1); // Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomizedSet.remove(2); // Returns false as 2 does not exist in the set.
randomizedSet.insert(2); // Inserts 2 to the set, returns true. Set now contains [1,2].
randomizedSet.getRandom(); // getRandom() should return either 1 or 2 randomly.
randomizedSet.remove(1); // Removes 1 from the set, returns true. Set now contains [2].
randomizedSet.insert(2); // 2 was already in the set, so return false.
randomizedSet.getRandom(); // Since 2 is the only number in the set, getRandom() will always return 2.
```

## Solution Approach

To implement the `RandomizedSet` class with O(1) time complexity for each function, we can use two data structures.

1. An array to store elements.
2. A hash table to store the mappings of elements to array indices.

### Design Idea

**Insertion**: Check if the element exists in the hash table. If it does not exist, append it to the end of the array and record the element's index in the hash table.

**Deletion**: Check if the element exists in the hash table. If it exists, remove it from the array. To ensure the time complexity of deletion is O(1), we can swap the element to be deleted with the last element of the array, then delete the last element, and update the indices of the related elements in the hash table.

Random Element Retrieval: Select a random element directly from the array.

### Implement

```js
class RandomizedSet {
    constructor() {
        this.nums = [];
        this.numToIndex = new Map();
    }

    /**
     * @param {number} val
     * @return {boolean}
     */
    insert(val) {
        // if val already exists in numToIndex, return false
        if (this.numToIndex.has(val)) {
            return false;
        }
        // Otherwise, append `val` to the end of `nums`, and record its index in `numToIndex`.
        this.numToIndex.set(val, this.nums.length);
        this.nums.push(val);
        return true;
    }

    /**
     * @param {number} val
     * @return {boolean}
     */
    remove(val) {
        if (!this.numToIndex.has(val)) {
            return false;
        }
        const index = this.numToIndex.get(val);
        const lastVal = this.nums[this.nums.length - 1];

        // Swap the element with the last one
        this.nums[index] = lastVal;
        this.numToIndex.set(lastVal, index);

        // Remove the last element
        this.nums.pop();
        this.numToIndex.delete(val);

        return true;
    }

    /**
     * @return {number}
     */
    getRandom() {
        // Select a random element directly from the array.
        const randomIndex = Math.floor(Math.random() * this.nums.length);
        return this.nums[randomIndex];
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * var obj = new RandomizedSet()
 * var param_1 = obj.insert(val)
 * var param_2 = obj.remove(val)
 * var param_3 = obj.getRandom()
 */
```



