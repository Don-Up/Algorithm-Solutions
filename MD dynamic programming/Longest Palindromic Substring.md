# [ Longest Palindromic Substring](https://leetcode.cn/problems/longest-palindromic-substring/)

Given a string s, return the longest palindromic substring in s.

> **Example 1:**
>
> ```
> Input: s = "babad"
> Output: "bab"
> Explanation: "aba" is also a valid answer.
> ```
>
> **Example 2:**
>
> ```
> Input: s = "cbbd"
> Output: "bb"
> ```

## Center Expansion Approach

To search for the longest palindromic substring of a string, we can use the approach of dynamic programming or center expansion. Here, we introduce the latter because its time complexity is O(n^2) and its implementation is simpler.

The palindrome is center-symmetric, so each position can act as the center for expansion on both sides to check if it is a palindrome. Since the length of a palindrome can be either an odd number or an even number, we need to check for cases centering on one character or two characters, respectively.

### Steps

1. Traverse each character and assume it is the palindrome center.
2. For each center, expand on both sides, check if the substring is a palindrome, record the lonest palindromic substring at the same time.
3. Consider two cases:
   1. Center on one character (odd-length palindrome).
   2. Center two characters (even-length palindrome).

```js
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
    if (s.length === 0) return "";
    
    // start and end are used to record the start and end of the lonest palindrome.
    let start = 0, end = 0;
    
    // expandAroundCenter expands from the center to both sides, finding the longest palindrome and returning its length.
    const expandAroundCenter = (s, left, right) => {
        // For each character s[i], calculate both the odd-length palindrome centering on it and the even-length palindrome centering on it and s[i+1].
        while (left >= 0 && right < s.length && s[left] === s[right]) {
            left--;
            right++;
        }
        return right - left - 1;
    };
    
    // Compare the lengths of the currently found palindromic substring and the previously recorded longest palindromic substring. If the former is longer, update start and end.
    for (let i = 0; i < s.length; i++) {
        let len1 = expandAroundCenter(s, i, i);   // odd-length
        let len2 = expandAroundCenter(s, i, i + 1); // even-length
        let len = Math.max(len1, len2);
        if (len > end - start) {
            start = i - Math.floor((len - 1) / 2);
            end = i + Math.floor(len / 2);
        }
    }
    // Finally, return the substring of `s` from `start` to `end`.
    return s.substring(start, end + 1);
};
```

