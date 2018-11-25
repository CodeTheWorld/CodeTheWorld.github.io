---
layout: article
title: 数组中的第K个最大元素-leetcode
tags: leetcode heap
key: leetcode-215-kth-largest-element-in-an-array
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/description/)

```go
/**
 思路：最小堆
*/
func findKthLargest(nums []int, k int) int {
    minHeap := &MinHeap{[]int{}, k, 0}

    for _, value := range nums {
        minHeap.Push(value)
    }

    return minHeap.Pop()
}

type MinHeap struct {
    heap  []int
    alloc int
    size  int
}

func (this *MinHeap) Push(value int) {
    if this.alloc > this.size {
        this.heap = append(this.heap, value)
        this.size++
        this.autoFixUp()
        return
    }
    minValue := this.Pop()
    if minValue >= value {
        this.Push(minValue)
    } else {
        this.Push(value)
    }
}

func (this *MinHeap) autoFixUp() {
    if 0 == this.size {
        return
    }
    value := this.heap[this.size-1]
    i := this.size - 1
    j := (i - 1) / 2
    for i > 0 {
        if this.heap[j] <= value {
            break
        }
        this.heap[i] = this.heap[j]
        i = j
        j = (i - 1) / 2
    }
    this.heap[i] = value
}

func (this *MinHeap) Pop() int {
    res := this.heap[0]
    this.heap[0] = this.heap[this.size-1]
    this.size--
    this.heap = this.heap[:this.size]
    this.autoFixDown()
    return res
}

func (this *MinHeap) autoFixDown() {
    if 0 == this.size {
        return
    }
    value := this.heap[0]
    i := 0
    j := 2*i + 1
    for j < this.size {
        if j+1 < this.size && this.heap[j] > this.heap[j+1] {
            j++
        }
        if value <= this.heap[j] {
            break
        }
        this.heap[i] = this.heap[j]
        i = j
        j = 2*i + 1
    }
    this.heap[i] = value
}
```
