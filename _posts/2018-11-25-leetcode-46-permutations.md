---
layout: article
title: 全排列-leetcode
tags: leetcode recursion
key: leetcode-46-permutations
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/permutations/description/)

```go
/**
思路：递归
*/
func permute(nums []int) [][]int {
    return permuteStart(nums, 0)
}

func permuteStart(nums []int, index int) [][]int {
    length := len(nums)
    res := [][]int{}
    if index == length {
        return res
    }
    for i := index; i < length; i++ {
        nums[i], nums[index] = nums[index], nums[i]
        nextRes := permuteStart(nums, index+1)
        nextLength := len(nextRes)
        if 0 == nextLength {
            res = append(res, []int{nums[index]})
        } else {
            for _, items := range nextRes {
                res = append(res, append(items, nums[index]))
            }
        }
        nums[i], nums[index] = nums[index], nums[i]
    }
    return res
}
```
