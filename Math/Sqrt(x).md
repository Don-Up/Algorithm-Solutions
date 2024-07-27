# [Sqrt(x)](https://leetcode.cn/problems/sqrtx/)

Given a non-negative integer `x`, return *the square root of* `x` *rounded down to the nearest integer*. The returned integer should be **non-negative** as well.

You **must not use** any built-in exponent function or operator.

- For example, do not use `pow(x, 0.5)` in c++ or `x ** 0.5` in python.

> **Example 1:**
>
> ```
> Input: x = 4
> Output: 2
> Explanation: The square root of 4 is 2, so we return 2.
> ```
>
> **Example 2:**
>
> ```
> Input: x = 8
> Output: 2
> Explanation: The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.
> ```

## Solution Approach

To calculate the square root of a non-negative integer `x` and return its integer part, you can use the binary search algorithm. Binary search is an efficient search algorithm that can find the result in logarithmic time.

### Steps

1. Initialize `left` and `right` pointers, pointing to 0 and `x` respectively.
2. Perform a binary searching and calculate the middle position `mid`.
3. Compare `mid` squared with `x`:
   1. If `mid` squared equals `x`, return `mid`.
   2. If `mid` squared is less than `x`, update `right` to `mid+1`.
   3. If `mid` squared is greater than `x`, update `right` to `mid-1`.
4. When `left` surpasses `right`, return `right`. At this point, `right` is the integer part of the result.

```js
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function(x) {
    if(x < 2) return x
    
    let left = 1
    let right = Math.floor(x/2)
    
    while(left <= right){
        const mid = Math.floor((left+right)/2)
        const midSquared = mid * mid
        
        if(midSquared === x){
            return mid
        } else if(midSquared < x){
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    
    return right
}
```

