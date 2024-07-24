# [Gas Station](https://leetcode.cn/problems/gas-station/)

There are `n` gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return *the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return* `-1`. If there exists a solution, it is **guaranteed** to be **unique**

 

**Example 1:**

```
Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
Output: 3
Explanation:
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.
```

**Example 2:**

```
Input: gas = [2,3,4], cost = [3,4,3]
Output: -1
Explanation:
You can't start at station 0 or 1, as there is not enough gas to travel to the next station.
Let's start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 0. Your tank = 4 - 3 + 2 = 3
Travel to station 1. Your tank = 3 - 3 + 3 = 3
You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3.
Therefore, you can't travel around the circuit once no matter where you start.
```

```js
/**
 * @param {number[]} gas
 * @param {number[]} cost
 * @return {number}
 */
var canCompleteCircuit = function(gas, cost) {

};
```

## Solution Approach

To solve the problem, we can use a greedy algorithm. Here is the conclusion: If starting from a certain gas station doesn't allow for completing the loop, then each of the gas stations before it cannot be a starting point either.

### Steps

1. Initialize the total gas amount `total_tank`, the current gas amount `current_tank`, and the starting gas station `start_index`.
2. Traverse all gas stations:
   1. Accumulate the gas amount and consumption at the current gas station.
   2. If `current_tank` turns negative, it means we can't reach the current gas station from the current `start_index`. We need to restart from the next gas station and reset `current_tank` to 0.
3. If the total gas amount is positive, it means completing the loop is possible; otherwise, return -1.

### Implementation Code

```js
/**
 * @param {number[]} gas
 * @param {number[]} cost
 * @return {number}
 */
var canCompleteCircuit = function(gas, cost) {
    const n = gas.length;
    // total_tank is used to determine whether the total gas amount can complete the circuit.
    // current_tank is used to record the gas amount from the starting gas station to the current gas station.
    // start_index indicates the gas station that is currently considered the starting point.
    let total_tank = 0, current_tank = 0, start_index = 0;
	
    for (let i = 0; i < n; i++) {
        // For each gas station, calculate the remaining gas amount to reach the next gas station, and update total_tank and current_tank.
        total_tank += gas[i] - cost[i];
        current_tank += gas[i] - cost[i];
        // If current_tank turns negative, it means we can't reach the current station from start_index. Update start_index to i + 1 and reset current_tank to 0.
        if (current_tank < 0) {
            start_index = i + 1;
            current_tank = 0;
        }
    }
	// If total_tank is greater than or equal to 0, it means we can complete the circuit, so return start_index. Otherwise, return -1 to indicate that completing the circuit is impossible.
    return total_tank >= 0 ? start_index : -1;
};

// 示例调用
console.log(canCompleteCircuit([1,2,3,4,5], [3,4,5,1,2])); // 输出：3
console.log(canCompleteCircuit([2,3,4], [3,4,3])); // 输出：-1
```

Using this greedy algorithm, we can solve the problem with O(n) time complexity.