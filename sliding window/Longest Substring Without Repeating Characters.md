# [Longest Substring Without Repeating Characters](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

Given a string `s`, find the length of the **longest** **substring** without repeating characters.



**Example 1:**

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function (s) {
}
```

## Solution Approach

### The idea of sliding window

1. Use two pointers, `left` and `right`, to indicate the left and right edges of the current window.
2. Use a `set` to store the characters of the current window.
3. Move `right` to expand the window. If a duplicate character is encountered, move `left` to narrow the window. Repeat this process until there are no duplicate characters within the window.

### Code implementation

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    // The starting position of `s`.
    let left = 0;
    // Initialize maxLength to 0, which will record the length of the longest substring.
    let maxLength = 0;
    // `set` is used to store characters within the current window.
    const set = new Set();
	
    // Traverse s and move right, checking if s[right] exists in the set each time.
    for (let right = 0; right < s.length; right++) {
        while (set.has(s[right])) {
            // If s[right] exists in the set, move left to narrow the window until the set no longer contains s[right].
            set.delete(s[left]);
            left++;
        }
        // Add s[right] to the set.
        set.add(s[right]);
        // Update maxLength to the current window's length, which is right - left + 1.
        maxLength = Math.max(maxLength, right - left + 1);
    }
	
    // Return maxLength, which is the length of the longest substring without duplicate characters.
    return maxLength;
};

// 示例调用
console.log(lengthOfLongestSubstring("abcabcbb")); // 输出：3
console.log(lengthOfLongestSubstring("bbbbb"));    // 输出：1
console.log(lengthOfLongestSubstring("pwwkew"));   // 输出：3
```

