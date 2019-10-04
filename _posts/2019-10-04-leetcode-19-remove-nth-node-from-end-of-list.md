---
layout: article
title: 删除链表的倒数第N个节点-leetcode
tags: leetcode
key: leetcode-19-remove-nth-node-from-end-of-list
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

```go
/**
 * 思路：递归
 * 在递归回退时，可得知当前node是倒数第几个
 */
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
