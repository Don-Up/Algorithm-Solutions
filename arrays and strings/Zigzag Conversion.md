# [Zigzag Conversion](https://leetcode.cn/problems/zigzag-conversion/)

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

> **Example 1:**
>
> ```
> Input: s = "PAYPALISHIRING", numRows = 3
> Output: "PAHNAPLSIIGYIR"
> ```
>
> **Example 2:**
>
> ```
> Input: s = "PAYPALISHIRING", numRows = 4
> Output: "PINALSIGYAHRPI"
> Explanation:
> P     I    N
> A   L S  I G
> Y A   H R
> P     I
> ```
>
> **Example 3:**
>
> ```
> Input: s = "A", numRows = 1
> Output: "A"
> ```

## Solution Approach

To arrange the given string `s` in a zigzag pattern according to the given `numRows` and generate a new string, we can use an approach to simulate the zigzag traversal.

### Idea

1. Initialization: If `numRows` is 1, return the string `s`. Otherwise, initialize an array `rows` to store each row of strings.
2. Traverse the string: use a pointer `curRow` to record the row where the current character should be placed, and use a direction variable `goingDown` to record whether to move up or down at present. 
   * When `curRow` is 0 or `numRows - 1`, change the direction.
3. Generate the result: When the string traversal is over, concatenate all rows in `rows` to generate the final result.

```js
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
    if (numRows === 1) return s;

    const rows = Array.from({ length: numRows }, () => "");
    let curRow = 0;
    let goingDown = false;

    for (let char of s) {
        rows[curRow] += char;
        if (curRow === 0 || curRow === numRows - 1) goingDown = !goingDown;
        curRow += goingDown ? 1 : -1;
    }

    return rows.join("");
};

// 示例调用
console.log(convert("PAYPALISHIRING", 3)); // 输出："PAHNAPLSIIGYIR"
console.log(convert("PAYPALISHIRING", 4)); // 输出："PINALSIGYAHRPI"
console.log(convert("A", 1)); // 输出："A"
```

