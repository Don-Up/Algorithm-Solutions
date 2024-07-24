# decode message

Your are given a 2-D array of characters. There is a hidden message in it.

```js
I B C A L K A
D R F C A E A
G H O E L A D 
```

The way to collect the message is as follows

1. start at top left
2. move diagonally down right
3. when cannot move any more, try to switch to diagonally up right
4. when cannot move any more, try switch to diagonally down right, repeat 3
5. stop when cannot neither move down right or up right. the character on the path is the message

for the input above, `IROCLED` should be returned.

*notes*

if no characters could be collected, return empty string

## Solution Approach

![image-20240708195748549](img\image-20240708195748549.png)

As shown in the figure, to solve this question, we need to traverse the two-dimensional array and collect these letters along the path. End up returning a string consisting of these letters.

### variable declarations

1. We need to declare a variable `row` to indicate the X-axis position of the current letter.
2. We need to declare a variable `col` to indicate the Y-axis position of the current letter.
3. We need to declare a variable `direction` to indicate the current path direction (down-right as 1 and up-right as -1).
4. We need to declare a string variable `result` to collect the letters along the path.
5. Finally, we declare two constants, `rows` and `columns`, to record the height and width of the two-dimensional array.

### Path Generation

Next, we should consider how to control the path generation using these variables.

#### DOWN-RIGHT

If the direction is down-right, increment the row by one and the column by one.

#### UP-RIGHT

If the direction is up-right, decrement the row by one and the column by one.

#### Change Direction

![image-20240708203853295](img\image-20240708203853295.png)

As shown in the figure, if the path goes beyond the array range (when row === rows or row === -1), we need to change the direction (direction *= -1) and reassign the row.

## Full Code

```js
/**
 * @param {string[][]} message
 * @return {string}
 */
function decode(message) {
    if (!message || message.length === 0 || message[0].length === 0) return '';

    const rows = message.length;
    const cols = message[0].length;
    let result = '';
    let direction = 1; // 1 for down-right, -1 for up-right

    let row = 0;
    let col = 0;

    while (row < rows && col < cols) {
        result += message[row][col];

        let newRow = row + direction;
        let newCol = col + 1;

        if (newRow === rows || newRow === -1) {
            direction *= -1; // Switch direction
            newRow = row + direction;
        }
        row = newRow;
        col = newCol;
    }

    return result;
}
```

