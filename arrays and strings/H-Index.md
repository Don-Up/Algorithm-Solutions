# H-Index

Given an array of integers `citations` where `citations[i]` is the number of citations a researcher received for their `ith` paper, return *the researcher's h-index*.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): The h-index is defined as the maximum value of `h` such that the given researcher has published at least `h` papers that have each been cited at least `h` times.

 

**Example 1:**

```
Input: citations = [3,0,6,1,5]
Output: 3
Explanation: [3,0,6,1,5] means the researcher has 5 papers in total and each of them had received 3, 0, 6, 1, 5 citations respectively.
Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations each, their h-index is 3.
```

**Example 2:**

```
Input: citations = [1,3,1]
Output: 1
```

 ```js
 /**
  * @param {number[]} citations
  * @return {number}
  */
 const hIndex = function(citations) {
    
 };
 ```

**Constraints:**

- `n == citations.length`
- `1 <= n <= 5000`
- `0 <= citations[i] <= 1000`

## Solution Approach

To calculate h-index, we need to find a maximum `h` such that there are at least `h` papers with `h` or more citations. The detailed steps are as follows:

**Sort the Citations**:

- Sort the array of citations in descending order. This way, we can easily find the h-index by iterating through the sorted list.

**Iterate Through the Sorted Citations**:

- Iterate through the sorted list and find the maximum value `h` such that there are at least `h` papers with `h` or more citations.

**Determine the h-index**:

- For each citation in the sorted list, check if it meets the condition for h-index. The condition is that the number of papers (`i+1`) is at least as large as the citation count at that position (`citations[i]`).

## Full Code

```js
const hIndex = function(citations) {
    // Sort the citations in descending order
    citations.sort((a, b) => b - a);
    
    let h = 0;
    
    // Iterate through the sorted list
    for (let i = 0; i < citations.length; i++) {
        // Check if the current citation count is at least the current index + 1
        // 6, 5, 3, 1, 0
        if (citations[i] >= i + 1) {
            h = i + 1;
        } else {
            break;
        }
    }
    
    return h;
};

// Example usage
console.log(hIndex([3, 0, 6, 1, 5])); // Output: 3
console.log(hIndex([1, 3, 1]));       // Output: 1

```

