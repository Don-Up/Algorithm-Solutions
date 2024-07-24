# [Add Two Numbers](https://leetcode.cn/problems/add-two-numbers/)

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

> **Example 1:**
>
> ![img](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)
>
> ```
> Input: l1 = [2,4,3], l2 = [5,6,4]
> Output: [7,0,8]
> Explanation: 342 + 465 = 807.
> ```
>
> **Example 2:**
>
> ```
> Input: l1 = [0], l2 = [0]
> Output: [0]
> ```
>
> **Example 3:**
>
> ```
> Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
> Output: [8,9,9,9,0,0,0,1]
> ```

## Solution Approach

To solve the problem of summing numbers represented by two linked lists and returning a new linked list to represent the result, we can use a bit-by-bit addition approach while considering the carry.

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    let num1 = l1.val.toString()
    while (l1.next){
        l1 = l1.next
        num1 = l1.val+num1
    }
    let num2 = l2.val.toString()
    while (l2.next){
        l2 = l2.next
        num2 = l2.val+num2
    }
    const arr = (BigInt(num1)+BigInt(num2)).toString()
    let node = null
    for (const string of arr) {
        node = new ListNode(string, node)
    }
    return node
};
```

