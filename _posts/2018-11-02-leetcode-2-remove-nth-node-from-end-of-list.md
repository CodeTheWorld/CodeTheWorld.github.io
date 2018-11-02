---
layout: article
title: 删除链表的倒数第N个节点-leetcode
tags: leetcode linked-list 快慢指针
key: leetcode-19-remove-nth-node-from-end-of-list
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/description/)

```go
type ListNode struct {
    Val  int
    Next *ListNode
}

/**
  思路：快慢指针
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
func removeNthFromEnd(head *ListNode, n int) *ListNode {
    newHead := &ListNode{0, head} // 新的head，预防head节点被删掉的情况
    slowPtr, quickPtr := newHead, head
    for ; n > 1 && nil != quickPtr; n-- { // 快指针先走n步
        quickPtr = quickPtr.Next
    }
    if nil == quickPtr { // 快指针到头，返回原链表
        return newHead.Next
    }
    for nil != quickPtr.Next { // 快慢指针齐步走，直到慢指针到达尽头
        quickPtr = quickPtr.Next
        slowPtr = slowPtr.Next
    }
    slowPtr.Next = slowPtr.Next.Next
    return newHead.Next
}
```
