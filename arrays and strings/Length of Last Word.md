# [Length of Last Word](https://leetcode.cn/problems/length-of-last-word/)

Given a string `s` consisting of words and spaces, return *the length of the **last** word in the string.*

A **word** is a maximal 

substring

 consisting of non-space characters only.



 

**Example 1:**

```
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
```

**Example 2:**

```
Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
```

**Example 3:**

```
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```

## Solution Approach

To get the length of the last word in a string, we can first trim the string and then iterate over it in reverse order. When `trimmedS[i]` is a space string, when can return `length`, otherwise increment `length` by one.

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
    let length = 0
    const trimmedS = s.trim()
    for(let i = trimmedS.length-1; i>=0; i--){
        if(trimmedS[i] !== " "){
            length++
        } else {
            return length
        }
    }
    return length
};
```

