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
    length := len(nums)
    res := [][]int{}
    if 0 == length {
        return res
    }

    for index, value := range nums {
        nextNums := []int{}
        nextNums = append(nextNums, nums[:index]...)
        nextNums = append(nextNums, nums[index+1:]...)
        items := permute(nextNums)
        itemLength := len(items)
        if 0 == itemLength {
            res = append(res, []int{value})
        } else {
            for _, item := range items {
                res = append(res, append(item, value))
            }
        }
    }
    return res
}
```
