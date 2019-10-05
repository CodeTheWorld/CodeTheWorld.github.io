---
layout: article
title: 复制带随机指针的链表-leetcode
tags: leetcode linked-list graph
key: leetcode-138-copy-list-with-random-pointer
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/copy-list-with-random-pointer/)

```go
/**
 * 思路：回溯
 */
type ListNode struct {
	Val    int
	Next   *ListNode
	Random *ListNode
}

func copyLinkedList(head *ListNode) *ListNode {
	nodeMap := make(map[*ListNode]*ListNode)
	return copyIter(head, nodeMap)
}

func copyIter(head *ListNode, nodeMap map[*ListNode]*ListNode) *ListNode {
	if head == nil {
		return nil
	}
	if node, ok := nodeMap[head]; ok {
		return node
	}
	newNode := &ListNode{head.Val, nil, nil}
	nodeMap[head] = newNode
	newNode.Next = copyIter(head.Next, nodeMap)
	newNode.Random = copyIter(head.Random, nodeMap)
	return newNode
}
```

```go
/**
 * 思路：迭代
 */
func copyLinkedList(head *ListNode) *ListNode {
	if head == nil {
		return nil
	}
	iter := head
	nodeMap := make(map[*ListNode]*ListNode)
	nodeMap[iter] = &ListNode{Val:iter.Val}
	for iter != nil {
		if iter.Next != nil {
			if _, ok := nodeMap[iter.Next]; !ok {
				nodeMap[iter.Next] = &ListNode{Val:iter.Next.Val}
			}
			nodeMap[iter].Next = nodeMap[iter.Next]
		}
		if iter.Random != nil {
			if _, ok := nodeMap[iter.Random]; !ok {
				nodeMap[iter.Random] = &ListNode{Val:iter.Random.Val}
			}
			nodeMap[iter].Random = nodeMap[iter.Random]
		}
		iter = iter.Next
	}
	return nodeMap[head]
}
```

```go
/**
 * 思路：使用链表代替map，起到通过旧节点查找新节点的作用
 */
func copyLinkedList(head *ListNode) *ListNode {
	if head == nil {
		return head
	}
	iter := head
	for iter != nil {
		newNode := &ListNode{Val:iter.Val}
		newNode.Next, iter.Next, iter = iter.Next, newNode, iter.Next
	}
	iter = head
	for iter != nil {
		if iter.Random != nil {
			iter.Next.Random = iter.Random.Next
		}
		iter = iter.Next.Next
	}
	newHead := head.Next
	iter = head
	for iter.Next != nil {
		iter.Next, iter = iter.Next.Next, iter.Next
	}
	return newHead
}
```
