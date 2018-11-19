---
layout: article
title: 设计循环队列-leetcode
tags: leetcode circular-queue
key: leetcode-622-design-circular-queue
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/design-circular-queue/description/)

```go
/**
 思路：利用slice实现
 */
type MyCircularQueue struct {
    queue    []int
    sizemask int
    head     int
    tail     int
}

func Constructor(k int) MyCircularQueue {
    return MyCircularQueue{make([]int, k+1), k + 1, 0, 0}
}

func (this *MyCircularQueue) EnQueue(value int) bool {
    if this.IsFull() {
        return false
    }
    this.queue[this.tail] = value
    this.tail = this.getLogicIndex(this.tail + 1)
    return true
}

func (this *MyCircularQueue) DeQueue() bool {
    if this.IsEmpty() {
        return false
    }
    this.head = this.getLogicIndex(this.head + 1)
    return true
}

func (this *MyCircularQueue) Front() int {
    if this.IsEmpty() {
        return -1
    }
    return this.queue[this.head]
}

func (this *MyCircularQueue) Rear() int {
    if this.IsEmpty() {
        return -1
    }
    return this.queue[this.getLogicIndex(this.tail-1)]
}

func (this *MyCircularQueue) IsEmpty() bool {
    return this.head == this.tail
}

func (this *MyCircularQueue) IsFull() bool {
    return this.head == this.getLogicIndex(this.tail+1)
}

func (this *MyCircularQueue) getLogicIndex(index int) int {
    if index < 0 {
        return index + this.sizemask
    }
    if index >= this.sizemask {
        return index - this.sizemask
    }
    return index
}
```
