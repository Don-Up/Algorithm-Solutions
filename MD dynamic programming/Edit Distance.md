# [Edit Distance](https://leetcode.cn/problems/edit-distance/)

Given two strings `word1` and `word2`, return *the minimum number of operations required to convert `word1` to `word2`*.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

> **Example 1:**
>
> ```
> Input: word1 = "horse", word2 = "ros"
> Output: 3
> Explanation: 
> horse -> rorse (replace 'h' with 'r')
> rorse -> rose (remove 'r')
> rose -> ros (remove 'e')
> ```
>
> **Example 2:**
>
> ```
> Input: word1 = "intention", word2 = "execution"
> Output: 5
> Explanation: 
> intention -> inention (remove 't')
> inention -> enention (replace 'i' with 'e')
> enention -> exention (replace 'n' with 'x')
> exention -> exection (replace 'n' with 'c')
> exection -> execution (insert 'u')
> ```

## Solution Approach

We can use dynamic programming to get the solution of the minimum operation count. These operations include insertion, deletion and replacement.

### The DP idea

We define a two-dimensional array `dp` where `dp[i][j]` indicates the required minimum operation count of converting the first `i` characters of `word1` into the first `j` characters of `word2`.

### The formula of state translation

* If `word1[i-1] == word2[j-1]`, `dp[i][j] = dp[i-1][j-1]`.

* If `word1[i-1] != word2[j-1]`, we need to consider these three operations:

  1. Insert a character: `dp[i][j] = dp[i][j-1] + 1`.
  2. Delete a character: `dp[i][j] = dp[i-1][j] + 1`.
  3. Replace a character: `dp[i][j] = dp[i-1][j-1] + 1`.

  Finally, choose the minimum value among the above three operations.

### Initialization

* `dp[0][0] = 0`, indicating the conversion from empty strings to empty strings requires 0 operations.
* `dp[i][0] = i`, indicating the conversion from the first `i` characters of `word1` to   an empty string requires `i` deletions.
* `dp[0][j] = j`, indicating the conversion from the first `j` characters of `word2` to an empty string requires `j` insertions.

### Implementation

```js
/**
 * @param {string} word1
 * @param {string} word2
 * @return {number}
 */
var minDistance = function(word1, word2) {
    const m = word1.length;
    const n = word2.length;
    
    // Initialize the DP array.
    const dp = Array.from({ length: m + 1 }, () => Array(n + 1).fill(0));
    
    // Initialize boundary conditions.
    for (let i = 1; i <= m; i++) {
        dp[i][0] = i;
    }
    for (let j = 1; j <= n; j++) {
        dp[0][j] = j;
    }
    
    // Fill the DP array.
    for (let i = 1; i <= m; i++) {
        for (let j = 1; j <= n; j++) {
            // If characters are same,
            if (word1[i - 1] === word2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                dp[i][j] = Math.min(
                    dp[i - 1][j] + 1,    // Delete
                    dp[i][j - 1] + 1,    // Insert
                    dp[i - 1][j - 1] + 1 // Replace
                );
            }
        }
    }
    
    return dp[m][n];
};

// Examples
console.log(minDistance("horse", "ros"));       // 3
console.log(minDistance("intention", "execution")); // 5
```





