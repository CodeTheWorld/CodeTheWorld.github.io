---
layout: article
title: 下一个排列-leetcode
tags: leetcode array
key: leetcode-31-next-permutation
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/next-permutation/description/)

```go
/**
  思路
    1.从后向前遍历，找到第一个比前面一个大的数的下标i
    2.从length-1开始向前遍历，找到第一个比i-1下标处数字大的j，然后break
    3.swap(nums[i-1],nums[j])
    4.将i之后的数组首尾倒置
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
func nextPermutation(nums []int) {
    length := len(nums)
    if 0 == length {
        return
    }
    var i, j int
    for i = length - 1; i > 0; i-- {
        if nums[i] > nums[i-1] {
            break
        }
    }
    if 0 != i {
        for j = length - 1; j >= i; j-- {
            if nums[j] > nums[i-1] {
                break
            }
        }
        nums[i-1], nums[j] = nums[j], nums[i-1]
    }
    for start := i; start <= (length+i-1)/2; start++ {
        nums[start], nums[length+i-1-start] = nums[length+i-1-start], nums[start]
    }
}
```
