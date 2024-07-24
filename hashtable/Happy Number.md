# [Happy Number](https://leetcode.cn/problems/happy-number/)

Write an algorithm to determine if a number `n` is happy.

A **happy number** is a number defined by the following process:

- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
- Those numbers for which this process **ends in 1** are happy.

Return `true` *if* `n` *is a happy number, and* `false` *if not*.

> **Example 1:**
>
> ```
> Input: n = 19
> Output: true
> Explanation:
> 12 + 92 = 82
> 82 + 22 = 68
> 62 + 82 = 100
> 12 + 02 + 02 = 1
> ```
>
> **Example 2:**
>
> ```
> Input: n = 2
> Output: false
> ```

```js
var isHappy = function(n) {
    // Intialize an empty set `seen` to store numbers have occured.
    const seen = new Set();
    
    // The condition of `while` loop is that `n` is not `1` and `n` hasn't occured in `seen`. 
    while (n !== 1 && !seen.has(n)) { 
        // add `n` to `seen`
        seen.add(n);
        // Convert `n` to a string and split it into a character array.
        // Use `recuce` to calculate the squared sum of the digits in `n`.
        n = n.toString().split("").reduce((sum, num) => sum + num * num, 0);
    }
    
    return n === 1;
};
```

