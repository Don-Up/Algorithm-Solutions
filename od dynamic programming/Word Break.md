# [Word Break](https://leetcode.cn/problems/word-break/)

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

 

**Example 1:**

```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

**Example 2:**

```
Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```

```js
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */
var wordBreak = function(s, wordDict) {

};
```

## Solution Approach

To solve the Word Break problem, you can use dynamic programming. The idea is to use a boolean array `dp` where `dp[i]` indicates whether the substring `s[0:i]`can be segmented into dictionary words.

### Initialize

* Create a boolean array `dp` of length `n+1` where `n` is the length of the string `s`. Initialize `dp[0]` to `true` because an empty string can always be segmented.

### Dynamic Programming

* Iterate through the string from `1` to `n`(length of the string `s`).
* For each position `i`, iterate form `0` to `i-1` to check if the substring `s[j:1]`is a word in `wordDict` and if `do[j]` is `true`.
* If both conditions are met, set `dp[i]`to `true` and break the inner loop.

### Result

* The value`dp[n]` will be  `true` if the entire string `s` can be segmented into words from `wordDict`, otherwise it will be `false`.

### Implementation

```js
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */
var wordBreak = function(s, wordDict) {
    // Use a`Set` to store the words in `wordDict` for faster lookup.
    const wordSet = new Set(wordDict)
    // `dp[0] = true` because am empty string is always segmentable.
    // [false, false, false]
    const dp = new Array(s.length+1).fill(false)
    // [true, false, false]
    dp[0]= true
    
    // the outer loop iterates over the length of the string `s`
    for(let i=1; i<=s.length; i++){
        // the inner loop checks all possible substrings ending at the current position `i`
        for(let j=0; j<i;j++){
            // If the substring `s[j:i]` is in `wordSet` and `dp[j]` is true, then `dp[i]` is set to true
            if(d[j] && wordSet.has(s.substring(j, i))){
                dp[i]=true
                break
            }
        }
    }
    
    // indicate if the whole string `s` can be segmented
    return dp[s.length]
}
```

