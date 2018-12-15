---
layout: article
title: 布隆过滤器-go实现
tags: 数据结构 bitmap
key: data-structure-bloom-filter
mathajx: false
---

<!--more-->

```go
/**
布隆过滤器
*/
type BloomFilter struct {
    words    []uint64
    sizemask int
}

func Constructor(size int) *BloomFilter {
    return &BloomFilter{make([]uint64, size/64+1), size - 1}
}

func (this *BloomFilter) Add(item string) {
    positions := this.getPosition(item)
    for _, position := range positions {
        word, bit := position/64, position%64
        this.words[word] |= (1 << bit) // 位或
    }
}

func (this *BloomFilter) Contains(item string) bool {
    positions := this.getPosition(item)
    for _, position := range positions {
        word, bit := position/64, position%64
        if this.words[word]&(1<<bit) == 0 {
            return false
        }
    }
    return true
}

func (this *BloomFilter) getPosition(item string) []uint32 {
    res := make([]uint32, 5)
    res[0] = murmur3.Sum32WithSeed([]byte(item), 1) % uint32(this.sizemask)
    res[1] = murmur3.Sum32WithSeed([]byte(item), 2) % uint32(this.sizemask)
    res[2] = murmur3.Sum32WithSeed([]byte(item), 3) % uint32(this.sizemask)
    res[3] = murmur3.Sum32WithSeed([]byte(item), 4) % uint32(this.sizemask)
    res[4] = murmur3.Sum32WithSeed([]byte(item), 5) % uint32(this.sizemask)
    return res
}

func (this *BloomFilter) Print() {
    fmt.Println(this.words)
}
```
