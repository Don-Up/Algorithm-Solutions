# [Best Time to Buy and Sell Stock IV](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/)

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day, and an integer `k`.

Find the maximum profit you can achieve. You may complete at most `k` transactions: i.e. you may buy at most `k` times and sell at most `k` times.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

> **Example 1:**
>
> ```
> Input: k = 2, prices = [2,4,1]
> Output: 2
> Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
> ```
>
> **Example 2:**
>
> ```
> Input: k = 2, prices = [3,2,6,5,0,3]
> Output: 7
> Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4. Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
> ```

## Solution Approach

To solve the maximum profit problem with up to `k` achievable transactions, we can use Dynamic Programming. The core of the problem is to maintain the achievable transaction times and the corresponding profit on a certain day.

## The idea of DP

1. Define profit:
   * `dp[i][j]` indicates the maximum profit of at most `j` transactions on day `i` (start from day 0).
2. The formula of state translation:
   * we need to consider whether to conduct the `jth` transaction on day `i`. 
   * If the `jth` transaction is not conducted, the state is `dp[i−1][j]`.
   * If the `jth` transaction is conducted, we need to buy in on a certain day and sell out on day `i`, the state is ` prices[i]−prices[m]+dp[m][j−1]prices[i] - prices[m] + dp[m][j-1]prices[i]−prices[m]+dp[m][j−1]` where `0≤m<i`.
   * Because the time complexity of the above formula is high, we can optimize it by defining a variable `max_diff = dp[m][j−1] - prices[m]` to record the optimal buy time `m`.
3. Initialization:
   * `dp[i][0]=0` indicates no transaction is conducted and the profit is 0.
   * `dp[0][j]=0` indicates the profit of any transaction conducted on day `0` is 0.
4. Implementation details:
   * We traverse transaction times on each day and, each time, use the above state transition formula to update the array `dp`.

```js
/**
 * @param {number} k
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(k, prices) {
    if (prices.length === 0) return 0;
    
    const n = prices.length;
    if (k >= n / 2) {
        // If k >= n/2, it can be considered as unlimited transactions
        let maxProfit = 0;
        for (let i = 1; i < n; i++) {
            if (prices[i] > prices[i - 1]) {
                maxProfit += prices[i] - prices[i - 1];
            }
        }
        return maxProfit;
    }

    const dp = Array.from({ length: k + 1 }, () => Array(n).fill(0));

    for (let t = 1; t <= k; t++) {
        let maxDiff = -prices[0];
        for (let d = 1; d < n; d++) {
            dp[t][d] = Math.max(dp[t][d - 1], prices[d] + maxDiff);
            maxDiff = Math.max(maxDiff, dp[t - 1][d] - prices[d]);
        }
    }

    return dp[k][n - 1];
};

// 示例调用
console.log(maxProfit(2, [2, 4, 1]));        // 输出：2
console.log(maxProfit(2, [3, 2, 6, 5, 0, 3])); // 输出：7
```

