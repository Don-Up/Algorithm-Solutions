# [Valid Parentheses](https://leetcode.cn/problems/valid-parentheses/)

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

> **Example 1:**
>
> ```
> Input: s = "()"
> Output: true
> ```
>
> **Example 2:**
>
> ```
> Input: s = "()[]{}"
> Output: true
> ```
>
> **Example 3:**
>
> ```
> Input: s = "(]"
> Output: false
> ```

## Solution Approach

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    const stack = []
    // Create a map to record the corresponding relationships of different types of parentheses.
    const map = {
        "(":")",
        "{": "}",
        "[":"]"
    }
    
    for (const char of s) {
        // If map[char] is true, it means char is the left part of a parentheses.
        if(map[char]){
            // Push char into stack.
            stack.push(char)
        } else {
            // Get top using stack.pop()
            const top = stack.pop()
            // If the left part is not corresponding to the right part, eturn false.
            if(map[top]!==char){
                return false
            }
        }
    }
    // Stack is empty or not determines if s is valid.
    return stack.length === 0
};
```

