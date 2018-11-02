---
layout: article
title: 移除元素-leetcode
tags: leetcode linked-list 快慢指针
key: leetcode-27-remove-element
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/remove-element/description/)

```go
/**
  思路：快慢指针
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
func removeElement(nums []int, val int) int {
    end := 0
    for _, value := range nums {
        if val == value {
            continue
        }
        nums[end] = value
        end++
    }
    return end
}
```
