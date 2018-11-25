---
layout: article
title: 全排列 II-leetcode
tags: leetcode recursion
key: leetcode-47-permutations-ii
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/permutations-ii/description/)

```go
/**
思路：递归
*/
func permuteUnique(nums []int) [][]int {
    length := len(nums)
    res := [][]int{}
    if 0 == length {
        return res
    }
    uniqMap := make(map[int]int)
    for index, value := range nums {
        if _, ok := uniqMap[value]; ok {
            continue
        }
        uniqMap[value] = 1
        nextNums := []int{}
        nextNums = append(nextNums, nums[:index]...)
        nextNums = append(nextNums, nums[index+1:]...)
        nextRes := permuteUnique(nextNums)
        if 0 == len(nextRes) {
            res = append(res, []int{value})
        } else {
            for _, items := range nextRes {
                res = append(res, append(items, value))
            }
        }
    }
    return res
}
```
