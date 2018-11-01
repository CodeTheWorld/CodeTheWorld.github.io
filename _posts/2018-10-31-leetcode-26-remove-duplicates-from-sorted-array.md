---
layout: article
title: 删除排序数组中的重复项-leetcode
tags: leetcode array 快慢指针
key: leetcode-26-remove-duplicates-from-sorted-array
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/description/)

```go
/**
  思路：快慢指针
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
func removeDuplicates(nums []int) int {
    length := len(nums)
    if length < 2 {
        return length
    }
    var i, j int
    for i, j = 0, 1; j < length; j++ { // i为慢指针，j为快指针
        if nums[i] == nums[j] {
            continue
        }
        i++
        nums[i] = nums[j]
    }
    return i + 1
}
```
