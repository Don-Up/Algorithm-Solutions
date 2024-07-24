# [Find the Index of the First Occurrence in a String](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/)

Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

 

**Example 1:**

```
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
```

**Example 2:**

```
Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.
```

```js
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
    const len = needle.length
    for (let i = 0; i < haystack.length; i++) {
        if(i+len > haystack.length){
            return -1
        }
        const currentStr = haystack.substring(i, len+i)
        if(currentStr === needle){
            return i
        }
    }
    return -1
};
```

## Solution Approach

To find the index of the first occurrence of `needle` in the string `haystack`, we can consider `needle` as a single unit. 

In the for loop of `haystack`, we use `haystack.substring(i, len + i)` to indicate the current string compared to `needle` for each iteration. If they are identical, we return `i`. If the sum of `i` and `needle.length` is greater than `haystack.length`, we can return -1 early. If the for loop finishes without finding the index, return -1.

