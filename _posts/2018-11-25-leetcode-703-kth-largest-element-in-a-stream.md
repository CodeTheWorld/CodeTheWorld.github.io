---
layout: article
title: 数据流中的第K大元素-leetcode
tags: leetcode heap
key: leetcode-703-kth-largest-element-in-a-stream
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/description/)

```go
/**
 思路：最小堆
*/
type KthLargest struct {
    heap  []int
    alloc int
    size  int
}


func Constructor(k int, nums []int) KthLargest {
    heap := KthLargest{[]int{}, k, 0}
    for _, value := range nums {
        heap.Add(value)
    }
    return heap
}


func (this *KthLargest) Add(val int) int {
    if this.alloc > this.size {
        this.heap = append(this.heap, val)
        this.size++
        this.autoFixUp()
        return this.heap[0]
    }
    minValue := this.Pop()
    if minValue <= val {
        minValue = val
    }
    return this.Add(minValue)
}

func (this *KthLargest) Pop() int {
    res := this.heap[0]
    this.heap[0] = this.heap[this.size-1]
    this.size--
    this.heap = this.heap[:this.size]
    this.autoFixDown()
    return res
}

func (this *KthLargest) autoFixUp() {
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

func (this *KthLargest) autoFixDown() {
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
