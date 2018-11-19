---
layout: article
title: 对链表进行插入排序-leetcode
tags: leetcode linked-list 插入排序 排序
key: leetcode-147-insertion-sort-list
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/insertion-sort-list/description/)

```go
/**
思路：插入排序
时间复杂度：O(n2)
空间复杂度：O(1)
*/
type ListNode struct {
    Val  int
    Next *ListNode
}

func insertionSortList(head *ListNode) *ListNode {
    newHead := &ListNode{0, nil}
    var node *ListNode
    for nil != head {
        node = head
        head = head.Next
        for iterator := newHead; iterator != nil; iterator = iterator.Next {
            if nil == iterator.Next || iterator.Next.Val >= node.Val {
                node.Next = iterator.Next
                iterator.Next = node
                break
            }
        }
    }
    return newHead.Next
}
```
