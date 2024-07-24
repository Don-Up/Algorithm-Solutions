# [Candy](https://leetcode.cn/problems/candy/)

There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.

Return *the minimum number of candies you need to have to distribute the candies to the children*.

 

**Example 1:**

```
Input: ratings = [1,0,2]
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.
```

**Example 2:**

```
Input: ratings = [1,2,2]
Output: 4
Explanation: You can allocate to the first, second and third child with 1, 2, 1 candies respectively.
The third child gets 1 candy because it satisfies the above two conditions.
```

```js
/**
 * @param {number[]} ratings
 * @return {number}
 */
var candy = function(ratings) {

};
```

## Solution Approach

To solve the problem, we can use a greedy algorithm.

Assign candies through two iterations. The first iteration goes from left to right, ensuring that each child with a higher score gets more candies than the child on their left. The second iteration goes from right to left, ensuring each child with a higher score gets more candies than the child on their right. Finally, sum the maximum values at each position of the two arrays.

### Steps

1. Create an array `candies` and initialize the candy amount for each child to 1.

   ```js
   const n = ratings.length;
   const candies = new Array(n).fill(1);
   ```

2. Traverse from left to right. If the current child's rating is higher than the previous child's, then the current child's candy amount is the previous child's amount plus one.

   ```js
   for (let i = 1; i < n; i++) {
       if (ratings[i] > ratings[i - 1]) {
           candies[i] = candies[i - 1] + 1;
       }
   }
   ```

3. Traverse from right to left. If the current child's rating is not higher than the next child's, then the current child's candy amount is the next child's amount plus one.

   ```js
   for (let i = n - 2; i >= 0; i--) {
       if (ratings[i] > ratings[i + 1]) {
           candies[i] = Math.max(candies[i], candies[i + 1] + 1);
       }
   }
   ```

4. Finally, calculate the sum of `candies`, which is the minimum number of candies needed.

   ```js
   return candies.reduce((a, b) => a + b, 0);
   ```

### Full Code

```js
/**
 * @param {number[]} ratings
 * @return {number}
 */
var candy = function(ratings) {
    const n = ratings.length;
    const candies = new Array(n).fill(1);
    
    // Traverse from left to right.
    for (let i = 1; i < n; i++) {
        if (ratings[i] > ratings[i - 1]) {
            candies[i] = candies[i - 1] + 1;
        }
    }
    
    // Traverse from right to left.
    for (let i = n - 2; i >= 0; i--) {
        if (ratings[i] > ratings[i + 1]) {
            candies[i] = Math.max(candies[i], candies[i + 1] + 1);
        }
    }
    
    // Calculate the sum
    return candies.reduce((a, b) => a + b, 0);
};

console.log(candy([1,0,2])); // Output: 5
console.log(candy([1,2,2])); // Output: 4
```





