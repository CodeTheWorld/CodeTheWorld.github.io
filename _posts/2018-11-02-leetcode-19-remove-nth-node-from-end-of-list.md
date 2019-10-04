---
layout: article
title: 删除链表的倒数第N个节点-leetcode
tags: leetcode linked-list 快慢指针 recursion
key: leetcode-19-remove-nth-node-from-end-of-list
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/description/)

```go
/**
  思路：快慢指针
  时间复杂度：O(n)
  空间复杂度：O(1)
*/

type ListNode struct {
    Val  int
    Next *ListNode
}

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

```go
/**
 * 思路：递归
 * 在递归回退时，可得知当前node是倒数第几个
 */
type ListNode struct {
    Val  int
    Next *ListNode
}

func removeNthFromEnd(head *ListNode, n int) *ListNode {
	node, _ := remove(head, n)
	return node
}

func remove(node *ListNode, n int) (*ListNode, int) {
	if node == nil {
		return nil, 0
	}
	next, depth := remove(node.Next, n)
	depth++
	if depth == n {
		return next, depth
	}
	if depth == n+1 {
		node.Next = next
	}
	return node, depth
}
```
