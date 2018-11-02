---
layout: article
title: 两数相加-leetcode
tags: leetcode linked-list
key: leetcode-02-add-two-numbers
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/add-two-numbers/description/)

```go
/**
  思路：大数相加，遍历，注意进位
  时间复杂度：O(n)
  空间复杂度：O(n)
*/
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    sum := &ListNode{}
    bit, flag, iterator := 0, 0, sum // bit 每位和，flag 进位标志 iterator 迭代器
    for nil != l1 || nil != l2 {
        bit = flag
        if nil != l1 {
            bit += l1.Val
            l1 = l1.Next
        }
        if nil != l2 {
            bit += l2.Val
            l2 = l2.Next
        }
        flag = bit / 10
        iterator.Next = &ListNode{bit % 10, nil}
        iterator = iterator.Next
    }
    return sum.Next
}
```
