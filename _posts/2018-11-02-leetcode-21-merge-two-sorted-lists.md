---
layout: article
title: 合并两个有序链表-leetcode
tags: leetcode linked-list
key: leetcode-21-merge-two-sorted-lists
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/merge-two-sorted-lists/description/)

```go
type ListNode struct {
    Val  int
    Next *ListNode
}

/**
  思路：链表遍历
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
    head := &ListNode{0, nil}
    ptr := head

    for nil != l1 && nil != l2 { // 两个链表都不为空
        if l1.Val <= l2.Val {
            ptr.Next = l1
            l1 = l1.Next
        } else {
            ptr.Next = l2
            l2 = l2.Next
        }
        ptr = ptr.Next
    }

    for nil != l1 { // l1不为空
        ptr.Next = l1
        l1 = l1.Next
        ptr = ptr.Next
    }
    for nil != l2 { // l2不为空
        ptr.Next = l2
        l2 = l2.Next
        ptr = ptr.Next
    }

    return head.Next
}
```
