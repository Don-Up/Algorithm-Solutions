# [Group Anagrams](https://leetcode.cn/problems/group-anagrams/)

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

> **Example 1:**
>
> ```
> Input: strs = ["eat","tea","tan","ate","nat","bat"]
> Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
> ```
>
> **Example 2:**
>
> ```
> Input: strs = [""]
> Output: [[""]]
> ```
>
> **Example 3:**
>
> ```
> Input: strs = ["a"]
> Output: [["a"]]
> ```

## Solution Approach

To group the anagrams together, we can use a hash table to store groups of each anagram. Specifically, we use the sorted version of each string as a key in the hash table and then add the original string to the list corresponding to its key.

```js
/**
 * @param {string[]} strs
 * @return {string[][]}
 */
var groupAnagrams = function(strs) { // ["eat","tea","tan","ate","nat","bat"]
    // Use a Map to store anagram groups, where the key is the sorted version of the strings and the value is the list of original strings.
    const map = new Map();

    for (let str of strs) {
        // For each string, sort its characters and join them to form sortedStr.
        const sortedStr = str.split('').sort().join('');
        // Check if sortedStr already exists in map. If not, initialize a new list.
        if (!map.has(sortedStr)) {
            map.set(sortedStr, []);
        }
        // Push the original string str into the list corresponding to sortedStr in the map.
        map.get(sortedStr).push(str);
    }

    // Convert all values of the map into an array using Array.from(map.values()) and return it.
    return Array.from(map.values());
};

// 示例调用
console.log(groupAnagrams(["eat", "tea", "tan", "ate", "nat", "bat"])); // 输出：[["bat"],["nat","tan"],["ate","eat","tea"]]
console.log(groupAnagrams([""])); // 输出：[[""]]
console.log(groupAnagrams(["a"])); // 输出：[["a"]]
```

