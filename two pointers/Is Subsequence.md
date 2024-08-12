# Is Subsequence

Given two strings `s` and `t`, return `true` *if* `s` *is a **subsequence** of* `t`*, or* `false` *otherwise*.

A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).

 

**Example 1:**

```
Input: s = "abc", t = "ahbgdc"
Output: true
```

**Example 2:**

```
Input: s = "axc", t = "ahbgdc"
Output: false
```

 ```js
 /**
  * @param {string} s
  * @param {string} t
  * @return {boolean}
  */
 var isSubsequence = function(s, t) {
 
 };
 ```

**Constraints:**

- `0 <= s.length <= 100`
- `0 <= t.length <= 104`
- `s` and `t` consist only of lowercase English letters.

 

**Follow up:** Suppose there are lots of incoming `s`, say `s1, s2, ..., sk` where `k >= 109`, and you want to check one by one to see if `t` has its subsequence. In this scenario, how would you change your code?

## Solution Approach

To determine if `s` is a subsequence of `t`, we need to check if each character of `s` occurs sequentially in `t`.

First and foremost, we need to handle some edge cases: If `s` is an empty string, we can return `true`. If `s.length` is equal to `t.length`, we can return `s === t`.

```js
if(s === ""){
    return true
}
if(s.length === t.length){
    return s === t
}
```

Next, we call `s.split("")` to get `sArr` and `t.split("")` to get `tArr`. We also declare a variable `start` initialized to 0 to record the position of the latest character found in `s`.

```js
const sArr = s.split("")
const tArr = t.split("")

let position = 0
```

Next, let's start a `for...of` loop on `tArr` to get `str`. In the iteration, if `str` is equal to `sArr[position]`, we increment `position` by one and then check if `position` is equal to `sArr.length`. If so, this means `s` is a subsequence of `t`, and we can directly return `true` to finish the function early.

```js
for (const str of tArr) {
    if(str === sArr[position]){
        position++
        if(position === sArr.length){
            return true
        }
    }
}
return position === sArr.length
```

At the end, when the loop is over, we can return `position === sArr.length` to complete the function.

## Full Code

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isSubsequence = function(s, t) {
    if(s === ""){
        return true
    }
    if(s.length === t.length){
        return s === t
    }
    const sArr = s.split("")
    const tArr = t.split("")

    let position = 0

    for (const str of tArr) {
        if(str === sArr[position]){
            position++
            if(position === sArr.length){
                return true
            }
        }
    }
    return position === sArr.length
};
```

```js
var isSubsequence = function(s, t) {
    const findResult = new Array(s.length).fill(false)
    let currentIndex = 0
    for(let char of t){
        if(char === s[currentIndex] && !findResult[currentIndex]){
            findResult[currentIndex] = true
            currentIndex++
        }
    }
    return currentIndex === s.length
};
```

