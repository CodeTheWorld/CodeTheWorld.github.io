---
layout: article
title: 两数之和-leetcode
tags: leetcode hashmap
key: leetcode-01-two-sum
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/two-sum/description/)

```go
/**
  思路：将数组中的index和value反向存储在hashmap中，通过hashmap O(1)的查找性能来查询数据
  时间复杂度 O(n)
  空间复杂度 O(n)
*/
func twoSum1(nums []int, target int) []int {
    length := len(nums)
    hashMap := make(map[int]int, length) // 利用hashmap存储value:key的数据
    for i, v := range nums {
        index, exist := hashMap[target-v]
        if !exist { // (target-value)未找到
            hashMap[v] = i
            continue
        }
        // 找到了(target-value)
        return []int{index, i}
    }
    return []int{}
}
```

```go
/**
  思路：将数组元素排序，从头尾向中间移动，定位元素
  时间复杂度 依赖排序算法
  空间复杂度 O(n)
*/
func twoSum2(nums []int, target int) []int {
    count := len(nums)
    tmpNums := make([]int, count)
    copy(tmpNums[:], nums)
    res := []int{}
    i := 0
    j := count - 1
    sort.Ints(nums) // 从小到大，排序

    for i < j {
        sum := nums[i] + nums[j]
        if sum > target {
            j--
            continue
        } else if sum < target {
            i++
            continue
        } else {
            break
        }
    }
    if i < j {
        for k, v := range tmpNums {
            if nums[i] == v || nums[j] == v {
                res = append(res, k)
            }
        }
    }

    return res
}
```
