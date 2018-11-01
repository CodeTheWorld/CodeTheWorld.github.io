---
layout: article
title: 搜索插入位置-leetcode
tags: leetcode array
key: leetcode-35-search-insert-position
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/search-insert-position/description/)


```go
/**
  思路：遍历
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
func searchInsert(nums []int, target int) int {
    for i, v := range nums {
        if target <= v {
            return i
        }
    }
    return len(nums)
}
```
