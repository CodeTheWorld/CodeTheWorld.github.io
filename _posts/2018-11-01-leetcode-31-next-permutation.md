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
    1.从前向后遍历
    2.标记发现的最后一个后面值比前面大的数的下标camel
    3.找对应camel后面比camel大但是比camel+1小的数据toSwap
    4.如果找到，则swap(toSwap, camel)
    5.对camel后面的数进行排序
  时间复杂度：O(n) + O(sort.Ints()) 依赖排序算法
  空间复杂度：O(1)
*/
func nextPermutation(nums []int) {
    length := len(nums)
    camel, toSwap := -1, 0

    for i := 0; i < length-1; i++ {
        if nums[i] < nums[i+1] {
            camel = i
            toSwap = i + 1
            continue
        }
        if camel >= 0 && nums[camel] < nums[i+1] && nums[i+1] < nums[toSwap] {
            toSwap = i + 1
        }
    }
    if camel >= 0 {
        nums[toSwap], nums[camel] = nums[camel], nums[toSwap]
    }
    sort.Ints(nums[camel+1:])
}
```

```go
/**
  思路
    1.从后向前遍历，找到第一个比前面一个大的数的下标i
    2.从i+1开始向后遍历，找到第一个比i-1下标处数字小的下标j，然后break
    3.swap(nums[i-1],nums[j-1])
    4.将i之后的数排序
  时间复杂度：O(n) + O(sort.Ints()) 依赖排序算法
  空间复杂度：O(1)
*/
func nextPermutation(nums []int) {
    length := len(nums)
    var i, j int
    for i = length - 1; i > 0; i-- { // 第1步
        if nums[i] > nums[i-1] {
            break
        }
    }
    if 0 != i {
        for j = i + 1; j < length; j++ { // 第2步
            if nums[j] <= nums[i-1] {
                break
            }
        }
        nums[j-1], nums[i-1] = nums[i-1], nums[j-1] // 第3步
    }
    sort.Ints(nums[i:]) // 第4步
}
```
