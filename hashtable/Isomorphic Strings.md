# [Isomorphic Strings](https://leetcode.cn/problems/isomorphic-strings/)

Given two strings `s` and `t`, *determine if they are isomorphic*.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

 

**Example 1:**

```
Input: s = "egg", t = "add"
Output: true
```

**Example 2:**

```
Input: s = "foo", t = "bar"
Output: false
```

**Example 3:**

```
Input: s = "paper", t = "title"
Output: true
```

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isIsomorphic = function(s, t) {
	
};
```

## Solution Approach

To determine if two strings are isomorphic, we should ensure the following points:

1. Each character in `s` can be mapped to a unique character in `t`.
2. Each character in `t` can also be mapped to a unique character in `s`.

We can use two hash tables to record the mapping relationships of each character. One hash table is used to record mappings from `s` to `t`, and the other is used to record mappings from `t` to `s`. Traverse both strings, and if any invalid mapping of characters is found, return `false`. If no invalid mapping is found by the end of the iteration, return `true`.

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isIsomorphic = function(s, t) {
    // If s and t have different lengths, return false.
    if (s.length !== t.length) return false;
	
    // mapST and mapTS are used to record character mappings from s to t and from t to s, respectively.
    const mapST = new Map();
    const mapTS = new Map();

    for (let i = 0; i < s.length; i++) {
        const charS = s[i];
        const charT = t[i];
		
        // Check if the mapping from `s[i]` to `s[j]` exists in `mapST`, return false if it exists but does not match.
        // Perform a similar check for `mapTS`.
        if ((mapST.has(charS) && mapST.get(charS) !== charT) || (mapTS.has(charT) && mapTS.get(charT) !== charS)) {
            return false;
        }
		
        // If mappings do not exist, add them to the mapping tables.
        mapST.set(charS, charT);
        mapTS.set(charT, charS);
    }

    return true;
};

// 示例调用
console.log(isIsomorphic("egg", "add")); // 输出：true
console.log(isIsomorphic("foo", "bar")); // 输出：false
console.log(isIsomorphic("paper", "title")); // 输出：true
```

