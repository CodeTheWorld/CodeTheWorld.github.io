---
layout: article
title: 用队列实现栈-leetcode
tags: leetcode design queue stack
key: leetcode-225-implement-stack-using-queues
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/implement-stack-using-queues/description/)

```go
type MyStack struct {
    queue    []int
    bakQueue []int
    length   int
}

func Constructor() MyStack {
    return MyStack{[]int{}, []int{}, 0}
}

func (this *MyStack) Push(x int) {
    this.bakQueue = append(this.bakQueue, this.queue...)
    this.queue = this.queue[0:0]
    this.queue = append(this.queue, x)
    this.queue = append(this.queue, this.bakQueue...)
    this.bakQueue = this.bakQueue[0:0]
    this.length++
}

func (this *MyStack) Pop() int {
    res := this.queue[0]
    this.queue = this.queue[1:]
    this.length--
    return res
}

func (this *MyStack) Top() int {
    return this.queue[0]
}

func (this *MyStack) Empty() bool {
    return this.length == 0
}
```
