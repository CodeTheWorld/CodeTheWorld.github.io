---
layout: article
title: 设计哈希集合-leetcode
tags: leetcode hashset
key: leetcode-705-design-hashset
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/design-hashset/description/)

```go
/**
 思路：利用slice来完成
*/
type MyHashSet struct {
    ht []int
}

func Constructor() MyHashSet {
    return MyHashSet{make([]int, 1000001)}
}

func (this *MyHashSet) Add(key int) {
    this.ht[key] = 1
}

func (this *MyHashSet) Remove(key int) {
    this.ht[key] = 0
}

func (this *MyHashSet) Contains(key int) bool {
    return 1 == this.ht[key]
}
```
