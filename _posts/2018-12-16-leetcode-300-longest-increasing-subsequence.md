---
layout: article
title: 最长上升子序列-leetcode
tags: leetcode DP
key: leetcode-300-longest-increasing-subsequence
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/longest-increasing-subsequence/description/)

```go
/**
思路：DP
时间复杂度：O(n2)
空间复杂度：O(n)
*/
func lengthOfLIS(nums []int) int {
    length := len(nums)
    if 1 >= length {
        return len(nums)
    }
    lengthArr := make([]int, length) // 长度数组
    lengthArr[0] = 1
    res := 0

    for i := 1; i < length; i++ {
        maxLen := 0
        for j := 0; j < i; j++ {
            if nums[i] > nums[j] && maxLen < lengthArr[j] { // 基于子串计算当前串长度
                maxLen = lengthArr[j]
            }
        }
        lengthArr[i] = maxLen + 1
        if lengthArr[i] > res {
            res = lengthArr[i]
        }
    }
    return res
}
```

```go
/**
思路：https://www.felix021.com/blog/read.php?1587
时间复杂度：O(nlogn)
空间复杂度：O(n)
*/
func lengthOfLIS(nums []int) int {
    length := len(nums)
    if length <= 1 {
        return length
    }
    minArr := make([]int, length)
    minArr[0] = nums[0]
    maxLen := 1
    for i := 1; i < length; i++ {
        index := upperSearch(minArr, 0, maxLen-1, nums[i])
        minArr[index] = nums[i]
        if maxLen < index+1 {
            maxLen = index + 1
        }
    }
    return maxLen
}

/**
在递增序列上查找第一个大于val的index
如果val大于序列中的所有值，则返回len(arr)
*/
func upperSearch(arr []int, start int, end int, val int) int {
    if val > arr[end] {
        return end + 1
    }
    for start < end {
        mid := (start + end) / 2
        if arr[mid] < val {
            start = mid + 1
        } else {
            end = mid
        }
    }

    return end
}
```
