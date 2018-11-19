---
layout: article
title: 设计链表-leetcode
tags: leetcode linked-list
key: leetcode-707-design-linked-list
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/design-linked-list/description/)

```go
/**
思路：单链表实现
*/
type SNode struct {
    Val  int
    Next *SNode
}

type MyLinkedList struct {
    head   *SNode
    length int
}

func Constructor() MyLinkedList {
    head := &SNode{-2, nil}
    return MyLinkedList{head, 0}
}

func (this *MyLinkedList) Get(index int) int {
    if this.length <= index {
        return -1
    }
    node := this.getNode(index)
    if nil == node {
        return -1
    }
    return node.Val
}

func (this *MyLinkedList) AddAtHead(val int) {
    this.AddAtIndex(0, val)
}

func (this *MyLinkedList) AddAtTail(val int) {
    this.AddAtIndex(this.length, val)
}

func (this *MyLinkedList) AddAtIndex(index int, val int) {
    if index > this.length {
        return
    }
    preNode := this.getNode(index - 1)
    if nil != preNode {
        newNode := &SNode{val, preNode.Next}
        preNode.Next = newNode
        this.length++
    }
}

func (this *MyLinkedList) DeleteAtIndex(index int) {
    if index >= this.length {
        return
    }
    preNode := this.getNode(index - 1)
    if nil != preNode {
        preNode.Next = preNode.Next.Next
        this.length--
    }
}

func (this *MyLinkedList) getNode(index int) *SNode {
    for ptr, i := this.head, -1; ptr != nil; ptr = ptr.Next {
        if i != index {
            i++
            continue
        }
        return ptr
    }
    return nil
}
```
