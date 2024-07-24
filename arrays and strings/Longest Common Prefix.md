# [Longest Common Prefix](https://leetcode.cn/problems/longest-common-prefix/)

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

 

**Example 1:**

```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## Solution Approach

 ```js
 /**
  * @param {string[]} strs ["flower","flow","flight"]
  * @return {string}
  */
 var longestCommonPrefix = function(strs) {
     // 字符串数组中长度最短的元素长度
     let prefix = ""
     for (let i = 0; i < strs[0].length; i++) {
         const ref = strs[0][i]
         if(strs.every(str => 
                       i <= str.length-1 && str[i] === ref)){
             prefix += ref
         } else {
             return prefix
         }
     }
     return prefix
 }
 ```

