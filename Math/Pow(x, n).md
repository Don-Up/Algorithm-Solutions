# [Pow(x, n)](https://leetcode.cn/problems/powx-n/)

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., `xn`).

> **Example 1:**
>
> ```
> Input: x = 2.00000, n = 10
> Output: 1024.00000
> ```
>
> **Example 2:**
>
> ```
> Input: x = 2.10000, n = 3
> Output: 9.26100
> ```
>
> **Example 3:**
>
> ```
> Input: x = 2.00000, n = -2
> Output: 0.25000
> Explanation: 2-2 = 1/22 = 1/4 = 0.25
> 
> Constraints:
> 
> -100.0 < x < 100.0
> -231 <= n <= 231-1
> n is an integer.
> Either x is not zero or n > 0.
> -104 <= xn <= 104
> ```

## Solution Approach

Handle negative indexes: If index `n` is negative, convert `x` to its reciprocal, and convert index `n` to positive.

```js
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
var myPow = function(x, n) {
    // If n equals 0, return 1.
    if (n === 0) return 1;
    
    if (n < 0) {
        x = 1 / x;
        n = -n;
    }
    // Use recursion to break down the problem into sub-problems.
    return n % 2 === 0 ? 
        // If n is a even number, recursively calculate (𝑥×𝑥)^𝑛/2
        myPow(x * x, Math.floor(n / 2)) :
  	// If n is an odd number, recursively calculate 𝑥×(𝑥×𝑥)^(n-1)/2
    x * myPow(x * x, Math.floor(n / 2));
};

// 示例调用
console.log(myPow(2.00000, 10)); // 输出：1024.00000
console.log(myPow(2.10000, 3));  // 输出：9.26100
console.log(myPow(2.00000, -2)); // 输出：0.25000
```

```js
var myPow = function(x, n) {
    if (n === 0) return 1;
    
    if (n < 0) {
        x = 1 / x;
        n = -n;
    }
    
    let result = 1;
    while (n > 0) {
        if (n % 2 !== 0) {
            // If n is an odd number, multiply the current x into result.
            result *= x;
        }
        // Update x to x times x.
        x *= x;
        // Update n to the floor of n divided by 2.
        n = Math.floor(n / 2);
    }
    return result;
};

// 示例调用
console.log(myPow(2.00000, 10)); // 输出：1024.00000
console.log(myPow(2.10000, 3));  // 输出：9.26100
console.log(myPow(2.00000, -2)); // 输出：0.25000
```

