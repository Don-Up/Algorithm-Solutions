# Ransom Note

Given two strings `ransomNote` and `magazine`, return `true` *if* `ransomNote` *can be constructed by using the letters from* `magazine` *and* `false` *otherwise*.

Each letter in `magazine` can only be used once in `ransomNote`.

 

**Example 1:**

```
Input: ransomNote = "a", magazine = "b"
Output: false
```

**Example 2:**

```
Input: ransomNote = "aa", magazine = "ab"
Output: false
```

**Example 3:**

```
Input: ransomNote = "aa", magazine = "aab"
Output: true
```

```js
/**
 * @param {string} ransomNote
 * @param {string} magazine
 * @return {boolean}
 */
var canConstruct = function(ransomNote, magazine) {
	const hashTable = {}
    for(const letter of magzine){
        if(hashTable[letter]){
            hashTable[letter]++
        } else {
            hashTable[letter] = 1
        }
    }
    
    for(const letter of ransomNote){
        if(!hashTable[letter]){
            return false
        } else {
            hashTable[letter]--
        }
    }
    
    return true
};
```

