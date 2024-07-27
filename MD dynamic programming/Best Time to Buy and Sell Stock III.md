# [Best Time to Buy and Sell Stock III](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/)

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Find the maximum profit you can achieve. You may complete **at most two transactions**.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

> **Example 1:**
>
> ```
> Input: prices = [3,3,5,0,0,3,1,4]
> Output: 6
> Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
> Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
> ```
>
> **Example 2:**
>
> ```
> Input: prices = [1,2,3,4,5]
> Output: 4
> Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
> Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
> ```
>
> **Example 3:**
>
> ```
> Input: prices = [7,6,4,3,1]
> Output: 0
> Explanation: In this case, no transaction is done, i.e. max profit = 0.
> ```

## Solution Approach

To calculate the maximum profit obtained from at most two transactions in a given stock price array, we can use the dynamic programming (DP) approach. We can utilize two arrays to record the maximum profits of conducting at most one transaction and two transactions in everyday.

### The idea of DP

1. Define two arrays `leftProfit` and  `rightProfit`.
   1. `leftProfit[i]` indicates the maximum profit of up to one transaction from the `0th` day to the `ith` day.
   2. `rightProfit[i]` indicates the maximum profit of up to one transaction from the `ith` day to the last day.
2. Traverse the `prices` array, fill `leftProfit` from left to right, fill `rightProfit` from right to left. 
3. Eventually, traverse each possible split point, add the values of positions corresponding to `leftProfit` and `rightProfit`, choose the maximum as the result.

### Impletation

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    if (prices.length < 2) return 0;
    
    const n = prices.length;
    const leftProfit = new Array(n).fill(0);
    const rightProfit = new Array(n).fill(0);

    // Calculate leftProfit
    let minPrice = prices[0];
    for (let i = 1; i < n; i++) {
        minPrice = Math.min(minPrice, prices[i]);
        leftProfit[i] = Math.max(leftProfit[i - 1], prices[i] - minPrice);
    }

    // Calculate rightProfit
    let maxPrice = prices[n - 1];
    for (let i = n - 2; i >= 0; i--) {
        maxPrice = Math.max(maxPrice, prices[i]);
        rightProfit[i] = Math.max(rightProfit[i + 1], maxPrice - prices[i]);
    }

    // Calculate the maximum profit by combining left and right profits
    let maxProfit = 0;
    for (let i = 0; i < n; i++) {
        maxProfit = Math.max(maxProfit, leftProfit[i] + rightProfit[i]);
    }

    return maxProfit;
};

// 示例调用
console.log(maxProfit([3,3,5,0,0,3,1,4])); // 输出：6
console.log(maxProfit([1,2,3,4,5]));       // 输出：4
console.log(maxProfit([7,6,4,3,1]));       // 输出：0
console.log(maxProfit([1]));               // 输出：0
```

