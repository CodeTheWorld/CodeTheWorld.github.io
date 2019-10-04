---
layout: article
title: 反转链表-leetcode
tags: leetcode linked-list
key: leetcode-206-reverse-linked-list
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/reverse-linked-list/submissions/)

```go
/**
 * 思路
 * 一个正向链表head和一个反向链表head
 */
 
type ListNode struct {
	Val  int
	Next *ListNode
}
 
func reverseList(head *ListNode) *ListNode {
	var reverseHead *ListNode
	for head != nil {
		reverseHead, head.Next, head = head, reverseHead, head.Next
	}
	return reverseHead
}
```

```go
/**
 * 思路：递归
 */
type ListNode struct {
	Val  int
	Next *ListNode
}

func reverseList(head *ListNode) *ListNode {
	if head == nil {
		return nil
    }
	tail := reverseList(head.Next)
	if tail == nil {
		return head
    }
	head.Next.Next = head
	head.Next = nil
	return tail
}
```
