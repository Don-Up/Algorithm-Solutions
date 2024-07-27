# [Add Binary](https://leetcode.cn/problems/add-binary/)

Given two binary strings `a` and `b`, return *their sum as a binary string*.

> **Example 1:**
>
> ```
> Input: a = "11", b = "1"
> Output: "100"
> ```
>
> **Example 2:**
>
> ```
> Input: a = "1010", b = "1011"
> Output: "10101"
> ```

## Solution Approach

To implement the addition of two binary strings, you can add them bit-by-bit while handling the carry.

1. Initialize pointers `i` and  `j` to point to the end of `a` and  `b` respectively.
2. Initialize a variable `carry` to 0, indicating the carry.
3. Initialize an empty result string.
4. Perform Addition bit-by-bit from right to left, until both iterations of two strings are over.
5. In each step, add up the two characters of the current bit and the carry, then calculate the result of the current bit and the new carry.
6. Add the result of the current bit to the beginning of `result`.
7. If any carry exists after traversal, add it to beginning of `result`.j

```js
/**
 * @param {string} a
 * @param {string} b
 * @return {string}
 */
var addBinary = function(a, b) {
    let i = a.length - 1;
    let j = b.length - 1;
    let carry = 0;
    let result = '';

    while (i >= 0 || j >= 0) {
        let sum = carry;
        
        if (i >= 0) {
            sum += parseInt(a[i], 10);
            i--;
        }

        if (j >= 0) {
            sum += parseInt(b[j], 10);
            j--;
        }

        result = (sum % 2) + result;
        carry = Math.floor(sum / 2);
    }

    if (carry > 0) {
        result = carry + result;
    }

    return result;
};

// 示例调用
console.log(addBinary("11", "1")); // 输出："100"
console.log(addBinary("1010", "1011")); // 输出："10101"
```

## 

