# [Palindrome Number](https://leetcode.cn/problems/palindrome-number/)

Given an integer `x`, return `true` *if* `x` *is a* palindrome, and `false` *otherwise*.

> **Example 1:**
>
> ```
> Input: x = 121
> Output: true
> Explanation: 121 reads as 121 from left to right and from right to left.
> ```
>
> **Example 2:**
>
> ```
> Input: x = -121
> Output: false
> Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
> ```
>
> **Example 3:**
>
> ```
> Input: x = 10
> Output: false
> Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
> ```

## Approach 1: String

1. Convert the integer into a string.
2. Check if the string is equal to its inverted string.

```js
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    if (x < 0) return false;
    const str = x.toString();
    const reversedStr = str.split('').reverse().join('');
    return str === reversedStr;
};

// 示例调用
console.log(isPalindrome(121)); // 输出：true
console.log(isPalindrome(-121)); // 输出：false
console.log(isPalindrome(10)); // 输出：false
```



## Approach 2: Invert integer

1. Negative numbers are not palindromes, so directly return `false`.
2. Reverse half of the integer, compare the first half of the original integer with the second half of the reversed integer, and check if they are equal.

```js
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    // Both negative numbers and numbers that end with 0 (excluding 0 itself) are not palindromes.
    if (x < 0 || (x % 10 === 0 && x !== 0)) return false; 
	
    // Intialize reversed to 0 to store the inverted number.
    let reversed = 0;
    // Extract the end digit of x bit-by-bit and construct reversed until x is less than or equal to reversed.
    while (x > reversed) {
        reversed = reversed * 10 + x % 10;
        x = Math.floor(x / 10);
    }

    // Compare x with reversed and check if they are equal, or whether x is equal to reversed after removing the last bit.
    return x === reversed || x === Math.floor(reversed / 10);
};

// 示例调用
console.log(isPalindrome(121)); // 输出：true
console.log(isPalindrome(-121)); // 输出：false
console.log(isPalindrome(10)); // 输出：false
```

