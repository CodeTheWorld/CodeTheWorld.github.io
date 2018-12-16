---
layout: article
title: 最大子序和-leetcode
tags: leetcode DP
key: leetcode-53-maximum-subarray
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/maximum-subarray/description/)

```go
/**
思路：DP，以当前节点为尾的数组的和为前面数组的最大和+当前节点的值
时间复杂度：O(n)
空间复杂度：O(n)
*/
func maxSubArray(nums []int) int {
    length := len(nums)
    if length <= 0 {
        return 0
    }
    sumArr := make([]int, length)
    sumArr[0] = nums[0]
    maxSum := nums[0]
    for i := 1; i < length; i++ {
        if sumArr[i-1] <= 0 {
            sumArr[i] = nums[i]
        } else {
            sumArr[i] = nums[i] + sumArr[i-1]
        }
        if sumArr[i] > maxSum {
            maxSum = sumArr[i]
        }
    }
    return maxSum
}
```
