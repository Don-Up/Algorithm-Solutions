# [Insert Interval](https://leetcode.cn/problems/insert-interval/)

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` *after the insertion*.

**Note** that you don't need to modify `intervals` in-place. You can make a new array and return it.

> **Example 1:**
>
> ```
> Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
> Output: [[1,5],[6,9]]
> ```
>
> **Example 2:**
>
> ```
> Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
> Output: [[1,2],[3,10],[12,16]]
> Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
> ```

## Solution Approach

To insert a new range `newInterval` into a list of non-overlapping and sorted intervals `intervals`, follow these steps:

1. Add all ranges that do not overlap with `newInterval` directly into `result`.
2. Merge all ranges that overlap with `newInterval`.
3. Add the merged `interval` into `result`.
4. Add ranges that do not overlap with `newInerval` and after it into `result.`

```js
/**
 * @param {number[][]} intervals
 * @param {number[]} newInterval
 * @return {number[][]}
 */
var insert = function(intervals, newInterval) {
    // To store the final range list.
    const result = [];
    // The index of the current iteration, initialized to 0.
    let i = 0;
    // The length of the range list.
    const n = intervals.length;

    // Add all ranges before `newInterval`.
    // Use a while loop to add all ranges that end before the beginning of newInterval into result.
    while (i < n && intervals[i][1] < newInterval[0]) {
        result.push(intervals[i]);
        i++;
    }

    // Merge overlapping ranges.
    // Use a while loop to merge all ranges that start before the end of newInterval.
    while (i < n && intervals[i][0] <= newInterval[1]) {
        // 💡Update the beginning and end of newInterval.
        newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
        newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
        i++;
    }
    // Add the merged newInterval.
    result.push(newInterval.);

    // Add all ranges after newInterval.
    while (i < n) {
        result.push(intervals[i]);
        i++;
    }

    return result;
};

// 示例调用
console.log(insert([[1,3],[6,9]], [2,5])); // 输出：[[1,5],[6,9]]
console.log(insert([[1,2],[3,5],[6,7],[8,10],[12,16]], [4,8])); // 输出：[[1,2],[3,10],[12,16]]
```

