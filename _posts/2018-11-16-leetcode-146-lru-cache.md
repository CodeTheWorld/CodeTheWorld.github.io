---
layout: article
title: LRU缓存机制-leetcode
tags: leetcode hashmap linked-list
key: leetcode-146-lru-cache
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/lru-cache/description/)

```go
/**
思路：使用hashmap保证O(1)访问；
    使用有序双向链表保证O(1)插入/删除
    每次get/put都将节点挪到链表头
*/
type Node struct {
    Key  int
    Val  int
    Pre  *Node
    Next *Node
}

type LRUCache struct {
    head     *Node
    tail     *Node
    hashMap  map[int]*Node
    capacity int
    size     int
}

func Constructor(capacity int) LRUCache {
    head := &Node{-1, -1, nil, nil}
    tail := &Node{-1, -1, nil, nil}
    head.Next = tail
    tail.Pre = head
    return LRUCache{head, tail, make(map[int]*Node), capacity, 0}
}

func (this *LRUCache) Get(key int) int {
    fmt.Println(this.hashMap)
    if node, ok := this.hashMap[key]; ok {
        this.removeFromList(node)
        this.insertIntoList(node)
        return node.Val
    }
    return -1
}

func (this *LRUCache) Put(key int, value int) {
    node, ok := this.hashMap[key]
    if ok { // 存在该key，则将其中链表中挪出，同时修改其值
        this.removeFromList(node)
        node.Val = value
    } else {
        if this.capacity == this.size { // Cache容量已满，复用尾节点
            node = this.tail.Pre
            this.removeFromList(node)
            delete(this.hashMap, node.Key)
            node.Key = key
            node.Val = value
        } else { // 创建新节点
            node = &Node{key, value, nil, nil}
            this.size++
        }
        this.hashMap[key] = node
    }
    this.insertIntoList(node)
}

/**
将节点从linked-list中移除
*/
func (this *LRUCache) removeFromList(node *Node) {
    node.Pre.Next = node.Next
    node.Next.Pre = node.Pre
}

/**
插入链表头
*/
func (this *LRUCache) insertIntoList(node *Node) {
    node.Next = this.head.Next
    this.head.Next.Pre = node
    node.Pre = this.head
    this.head.Next = node
}
```
