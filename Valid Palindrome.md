# Valid Palindrome

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` *if it is a **palindrome**, or* `false` *otherwise*.

 

**Example 1:**

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

**Example 2:**

```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

**Example 3:**

```
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```

 ```js
 /**
  * @param {string} s
  * @return {boolean}
  */
 var isPalindrome = function(s) {
 }
 ```

**Constraints:**

- `1 <= s.length <= 2 * 105`
- `s` consists only of printable ASCII characters.

## Solution  Approach

To determine if a string is a palindrome, we first need to convert the string into an array that contains only letters and numbers.

Declare an array `filteredArray` to store elements that meet the specified criteria.

We start a `for...of` loop on `s.splite("")` and get `char` . In each iteration, if `char` is either a letter or a number, we push it into `filteredArray`. We can determine if `char` is a letter by passing it into `/^[a-zA-Z]$/.test(char)`, and determine if `char` is a number by using `!isNaN(parseInt(char))`.

> `/^[a-zA-Z]$/` can be read out as Forward slash, caret, left bracket, a, hyphen, z, A, hyphen, Z, right bracket, dollar, forward slash.

 ```js
 const filteredArray = []
 for (let char of s.split("")) {
     if(/^[a-zA-Z]$/.test(char) || !isNaN(parseInt(char)) ){
         filteredArray.push(char.toLowerCase())
     }
 }
 ```

Next, we declare a variable `start` initialized to 0 and another variable `end` initialized to `filteredArray.length - 1`.

After the declarations, we start a `while` loop that continues as long as `start` is less than `end`. In the iteration, we check if `filteredArray[start]` is not equal to `filteredArray[end]`, and if so, we return `false`. Otherwise, we increment `start` by one and decrement `end` by one.

If each iteration passes successfully, we can return `true` at the end.

## Full Code

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
    const filteredArray = []
    for (let char of s.split("")) {
        if(/^[a-zA-Z]$/.test(char) || !isNaN(parseInt(char)) ){
            filteredArray.push(char.toLowerCase())
        }
    }
    let start = 0
    let end = filteredArray.length-1
    while (start<end){
        if(filteredArray[start] !== filteredArray[end]){
            return false
        }
        start++
        end--
    }
    return true
};
```

