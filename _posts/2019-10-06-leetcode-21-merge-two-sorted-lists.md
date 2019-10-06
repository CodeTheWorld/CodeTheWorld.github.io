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
  思路：迭代
  时间复杂度：O(n+m)
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
    if l1 != nil { // l1不为空
        ptr.Next = l1
    }
    if l2 != nil { // l2不为空
        ptr.Next = l2
    }

    return head.Next
}
```

```go
/**
 * 思路：递归
 * 时间复杂度：O(n+m)
 * 空间复杂度：O(n+m)
 */
func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
	if l1 == nil {
		return l2
	}
	if l2 == nil {
		return l1
	}
	if l1.Val < l2.Val {
		l1.Next = mergeTwoLists(l1.Next, l2)
		return l1
	} else {
		l2.Next = mergeTwoLists(l1, l2.Next)
		return l2
	}
}
```
