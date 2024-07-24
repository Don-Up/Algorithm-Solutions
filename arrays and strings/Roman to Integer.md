# [Roman to Integer](https://leetcode.cn/problems/roman-to-integer/)

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two ones added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.



**Example 1:**

```
Input: s = "III"
Output: 3
Explanation: III = 3.
```

**Example 2:**

```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

**Example 3:**

```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

```js
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {

};
```

## Full Code

```js
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
    const romanMap = {
        "I":1,
        "V":5,
        "X":10,
        "L":50,
        "C":100,
        "D":500,
        "M":1000
    }

    let total = 0
    let prevValue = 0

    // Consideration:Can we use a forward loop here.
    // It's obviously impossible, because you must determine whether the current value should be added or subtracted based on the next number.
    for(let i = s.length-1; i>=0; i--){
        const currentValue = romanMap[s[i]]
        if(currentValue < prevValue){
            // If the left value is less than the right value, it means the current value needs to be subtracted from total.
            total -= currentValue
        } else{
            // Otherwise add the current value to `total`
            total += currentValue
        }
        // update prevValue
        prevValue = currentValue
    }
    
    return total

};
```

```
MCMXCIV
M = 1000, CM = 900(1000-100), XC = 90(100-10) and IV = 4(5-1).

```

![image-20240721094112409](assets/image-20240721094112409.png)