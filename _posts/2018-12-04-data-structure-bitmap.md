---
layout: article
title: 位图-go实现
tags: 数据结构 bitmap
key: data-structure-bitmap
mathajx: false
---

<!--more-->

```go
/**
位图
*/
type BitMap struct {
    length int      // 已存储元素个数
    words  []uint64 // 位图数组
}

func Construct() *BitMap {
    return &BitMap{}
}

func (this *BitMap) Has(num int) bool {
    word, bit := num/64, uint(num%64)
    return word < len(this.words) && this.words[word]&(1<<bit) != 0
}

func (this *BitMap) Add(num int) {
    word, bit := num/64, uint(num%64) // word:对应uint64的个数；bit:word内的位置
    for i := len(this.words); i <= word; i++ {
        this.words = append(this.words, 0)
    }
    this.words[word] |= (1 << bit) // 位或
    this.length++
}

func (this *BitMap) Len() int {
    return this.length
}

func (this *BitMap) Print() {
    for i, j := 0, 0; i < this.length; i++ {
        for ; ; j++ {
            word, bit := j/64, uint(j%64)
            if this.words[word]&(1<<bit) != 0 {
                fmt.Println(j)
                j++
                break
            }
        }
    }
}
```
