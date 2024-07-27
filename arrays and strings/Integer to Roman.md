# [Integer to Roman](https://leetcode.cn/problems/integer-to-roman/)

Seven different symbols represent Roman numerals with the following values:

| Symbol | Value |
| ------ | ----- |
| I      | 1     |
| V      | 5     |
| X      | 10    |
| L      | 50    |
| C      | 100   |
| D      | 500   |
| M      | 1000  |

Roman numerals are formed by appending the conversions of decimal place values from highest to lowest. Converting a decimal place value into a Roman numeral has the following rules:

- If the value does not start with 4 or 9, select the symbol of the maximal value that can be subtracted from the input, append that symbol to the result, subtract its value, and convert the remainder to a Roman numeral.
- If the value starts with 4 or 9 use the **subtractive form** representing one symbol subtracted from the following symbol, for example, 4 is 1 (`I`) less than 5 (`V`): `IV` and 9 is 1 (`I`) less than 10 (`X`): `IX`. Only the following subtractive forms are used: 4 (`IV`), 9 (`IX`), 40 (`XL`), 90 (`XC`), 400 (`CD`) and 900 (`CM`).
- Only powers of 10 (`I`, `X`, `C`, `M`) can be appended consecutively at most 3 times to represent multiples of 10. You cannot append 5 (`V`), 50 (`L`), or 500 (`D`) multiple times. If you need to append a symbol 4 times use the **subtractive form**.

Given an integer, convert it to a Roman numeral.

 

**Example 1:**

**Input:** num = 3749

**Output:** "MMMDCCXLIX"

**Explanation:**

```
3000 = MMM as 1000 (M) + 1000 (M) + 1000 (M)
 700 = DCC as 500 (D) + 100 (C) + 100 (C)
  40 = XL as 10 (X) less of 50 (L)
   9 = IX as 1 (I) less of 10 (X)
Note: 49 is not 1 (I) less of 50 (L) because the conversion is based on decimal places
```

**Example 2:**

**Input:** num = 58

**Output:** "LVIII"

**Explanation:**

```
50 = L
 8 = VIII
```

**Example 3:**

**Input:** num = 1994

**Output:** "MCMXCIV"

**Explanation:**

```
1000 = M
 900 = CM
  90 = XC
   4 = IV
```

## Approach Solution

To convert an integer into a Roman numeral, we can use the greedy algorithm according to the rules of Roman numerals. Process each Roman numeral in order from largest to smallest. When the integer `num` is greater than or equal to the value of the current symbol, add the symbol to the result string and subtract its value from `num`.

```js
/**
 * @param {number} num
 * @return {string}
 */
var intToRoman = function(num) {
    // 1. Define arrays of digits and symbols
    
    // val stores integers corresponding to Roman numerals from largest to smallest.
    const val = [
        1000, 900, 500, 400, 100, 90, 
        50, 40, 10, 9, 5, 4, 1
    ];
    
    // symbols stores corresponding symbols of roman numerals
    const symbols = [
        "M", "CM", "D", "CD", "C", "XC", 
        "L", "XL", "X", "IX", "V", "IV", "I"
    ];
    
    // 2. Traverse and construct the roman numeral string.
    
    // Initialize an empty string `roman` to store the final roman numeral.
    let roman = ''; 
    // Use a loop to traverse `val`, for each value `val[i]`, check if the current `num` is greater than or equal to this value.
    for (let i = 0; i < val.length; i++) {
        while (num >= val[i]) {
            // If so, add symbols[i] to roman, then process the next symbol, and subtract `val[i]`.
            roman += symbols[i];
            num -= val[i];
        }
    }
    //
    return roman;
};

// 示例调用
console.log(intToRoman(3));    // 输出："III"
console.log(intToRoman(4));    // 输出："IV"
console.log(intToRoman(9));    // 输出："IX"
console.log(intToRoman(58));   // 输出："LVIII"
console.log(intToRoman(1994)); // 输出："MCMXCIV"
```



