# [Valid Anagram](https://leetcode.cn/problems/valid-anagram/)

Given two strings `s` and `t`, return `true` *if* `t` *is an anagram of* `s`*, and* `false` *otherwise*.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

> **Example 1:**
>
> ```
> Input: s = "anagram", t = "nagaram"
> Output: true
> ```
>
> **Example 2:**
>
> ```
> Input: s = "rat", t = "car"
> Output: false
> ```

## Solution Approach

Use two hash tables (objects) to record the occurrences of each character in two strings, then compare the two hash tables to check if they are identical.

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
    if (s.length !== t.length) return false;
	
     // Initialize two empty objects, countS and countT, to record the occurrences of characters in s and t, respectively.
    const countS = {};
    const countT = {};
	
    // Traverse s and t, updating the occurrences of corresponding characters in countS and countT.
    
    for (let char of s) {
        countS[char] = (countS[char] || 0) + 1;
    }

    for (let char of t) {
        countT[char] = (countT[char] || 0) + 1;
    }
	
    // Compare countS and countT to check if the count of each character is the same. If so, it means that s is an anagram of t.
    for (let char in countS) {
        if (countS[char] !== countT[char]) {
            return false;
        }
    }

    return true;
};

// 示例调用
console.log(isAnagram("anagram", "nagaram")); // 输出：true
console.log(isAnagram("rat", "car")); // 输出：false
```

