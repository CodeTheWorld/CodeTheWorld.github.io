---
layout: article
title: 前K个高频元素-leetcode
tags: leetcode heap
key: leetcode-347-top-k-frequent-elements
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/top-k-frequent-elements/description/)

```go
/**
 思路：最小堆
*/
func topKFrequent(nums []int, k int) []int {
    freqMap := make(map[int]int)
    for _, val := range nums {
        freqMap[val]++
    }

    minHeap := &MinHeap{[]int{}, freqMap, k, 0}

    for value, _ := range freqMap {
        minHeap.Push(value)
    }

    return minHeap.PopAll()
}

type MinHeap struct {
    heap  []int
    kvMap map[int]int
    alloc int
    size  int
}

func (this *MinHeap) PopAll() []int {
    res := []int{}
    for this.size > 0 {
        value := this.Pop()
        res = append(res, value)
    }
    return res
}

func (this *MinHeap) Push(value int) {
    if this.alloc > this.size {
        this.heap = append(this.heap, value)
        this.size++
        this.autoFixUp()
        return
    }
    minValue := this.Pop()
    if this.kvMap[minValue] >= this.kvMap[value] {
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
        if this.kvMap[this.heap[j]] <= this.kvMap[value] {
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
        if j+1 < this.size && this.kvMap[this.heap[j]] > this.kvMap[this.heap[j+1]] {
            j++
        }
        if this.kvMap[value] <= this.kvMap[this.heap[j]] {
            break
        }
        this.heap[i] = this.heap[j]
        i = j
        j = 2*i + 1
    }
    this.heap[i] = value
}
```
