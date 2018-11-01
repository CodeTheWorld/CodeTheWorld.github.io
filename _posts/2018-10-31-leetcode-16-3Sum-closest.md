---
layout: article
title: 最接近的三数之和-leetcode
tags: leetcode array 双指针
key: leetcode-16-3Sum-closest
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/3sum-closest/description/)

```go
/**
  思路
    1.将数组排序
    2.fix一个数
    3.双指针左右夹逼，寻找最合适的值
  时间复杂度：O(n2)
  空间复杂度：O(1)
*/
func threeSumClosest(nums []int, target int) int {
    length, closest, gap, sum := len(nums), 0, 0, 0
    sort.Ints(nums) // 排序

    for i := 0; i < length-2; i++ { // fix一个值
        for left, right := i+1, length-1; left < right; { // 双指针从两边向中间移动
            sum = nums[left] + nums[right] + nums[i]
            diff := sum - target // 计算差值diff
            if diff > 0 {
                right--
            } else if diff < 0 {
                left++
                diff *= -1
            } else {
                return sum
            }
            if diff < gap || 0 == gap {
                gap = diff
                closest = sum
            }
        }
    }

    return closest
}
```
