# [Merge Intervals](https://leetcode.cn/problems/merge-intervals/)

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return *an array of the non-overlapping intervals that cover all the intervals in the input*.

> **Example 1:**
>
> ```
> Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
> Output: [[1,6],[8,10],[15,18]]
> Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
> ```
>
> **Example 2:**
>
> ```
> Input: intervals = [[1,4],[4,5]]
> Output: [[1,5]]
> Explanation: Intervals [1,4] and [4,5] are considered overlapping.
> ```

## Solution Approach

We can follow the following steps to merge all overlapping ranges:

1. First, sort all ranges by their starting positions.
2. Initialize a resulting array `result` and add the first range to `result`.
3. Traverse the remaining ranges, and for each range:
   - If the start of the current range is after the end of the last range in `result`, add the current range to `result`.
   - Otherwise, merge the current range with the last range in `result`.

```js
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function(intervals) {
    if (intervals.length === 0) return [];

    // Sort intervals by their starting positions.
    intervals.sort((a, b) => a[0] - b[0]);
	
    // Initialize the resulting array `result`.
    const result = [];
    // Set currentInterval to the first interval in the sorted intervals.
    let currentInterval = intervals[0];
	
    // Traverse the remaining intervals.
    for (let i = 1; i < intervals.length; i++) {
        const [currentStart, currentEnd] = currentInterval;
        const [nextStart, nextEnd] = intervals[i];
		
        // For each interval, check if it is overlapping with `currentInterval`.
        if (nextStart <= currentEnd) {
            // If they are overlapping, merge them and update currentInterval.
            currentInterval = [currentStart, Math.max(currentEnd, nextEnd)];
        } else {
            // If they are not overlapping, push currentInterval into result, and update currentInterval to intervals[i].
            result.push(currentInterval);
            currentInterval = intervals[i];
        }
    }

    // Push the last interval into result.
    result.push(currentInterval);

    return result;
};

// 示例调用
console.log(merge([[1,3],[2,6],[8,10],[15,18]])); // 输出：[[1,6],[8,10],[15,18]]
console.log(merge([[1,4],[4,5]])); // 输出：[[1,5]]
```

