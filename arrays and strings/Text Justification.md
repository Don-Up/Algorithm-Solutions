# [Text Justification](https://leetcode.cn/problems/text-justification/)

Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

**Note:**

- A word is defined as a character sequence consisting of non-space characters only.
- Each word's length is guaranteed to be greater than `0` and not exceed `maxWidth`.
- The input array `words` contains at least one word.

 

**Example 1:**

```
Input: words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

**Example 2:**

```
Input: words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16
Output:
[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]
Explanation: Note that the last line is "shall be    " instead of "shall     be", because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified because it contains only one word.
```

**Example 3:**

```
Input: words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20
Output:
[
  "Science  is  what we",
  "understand      well",
  "enough to explain to",
  "a  computer.  Art is",
  "everything  else  we",
  "do                  "
]
```

 

**Constraints:**

- `1 <= words.length <= 300`
- `1 <= words[i].length <= 20`
- `words[i]` consists of only English letters and symbols.
- `1 <= maxWidth <= 100`
- `words[i].length <= maxWidth`



## Solution Approach

To solve the problem, we need to use a greedy algorithm to place as many words as possible in each line, ensuring the length of each line is exactly `maxWidth`. Additionally, we need to handle white spaces between words to distribute them as evenly as possible.

## Steps

1. ### Variable Initialization

   * An array `lines` to store the result.
   * A temporary array `currentLine` to store words of the current line.
   * A variable  `currentLength` to store the total character length of the current line.

2. ### Traverse the word array

   * For each word, check if the length of the current line after adding the word surpasses `maxWidth`.
   * If it surpasses `maxWidth`, handle the words of the current line and add them to `lines`.
   * The way to handle the words of the current line is to justify them by adding white spaces as needed.
   * Add the current word to `currentLine` and update `currentLength`.

3. ### Handle the last line

   * The last line need to be left-aligned, so add words directly and use white spaces to fill the length to `maxWidth`.

## Code Implementation

```js
/**
 * @param {string[]} words
 * @param {number} maxWidth
 * @return {string[]}
 */
var fullJustify = function(words, maxWidth) {
    // to store results of each line
    const lines = [];
    // to store words of the current line
    let currentLine = [];
    // to store the total character length of the current line (excluding spaces)
    let currentLength = 0;
	
    // traverse the word array
    for (const word of words) {
        // Check if adding the current word exceeds the maxWidth
        if (currentLength + word.length + currentLine.length > maxWidth) {
            // Justify the current line
            for (let i = 0; i < maxWidth - currentLength; i++) {
                // Use modulus operation to evenly distribute white spaces between each word.
                currentLine[i % (currentLine.length - 1 || 1)] += ' ';
            }
            lines.push(currentLine.join(''));
            currentLine = [];
            currentLength = 0;
        }
        currentLine.push(word);
        currentLength += word.length;
    }

    // Handle the last line
    const lastLine = currentLine.join(' ');
    lines.push(lastLine + ' '.repeat(maxWidth - lastLine.length));

    return lines;
};

// 示例调用
console.log(fullJustify(["This", "is", "an", "example", "of", "text", "justification."], 16));
console.log(fullJustify(["What","must","be","acknowledgment","shall","be"], 16));
console.log(fullJustify(["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], 20));

```



