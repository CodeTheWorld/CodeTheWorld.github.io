---
layout: article
title: 第k个排列-leetcode
tags: leetcode 康托展开
key: leetcode-60-permutation-sequence
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/permutation-sequence/description/)

```go
/**
思路：康托展开
时间复杂度：O(n2)，维护剩余字符数组的成本
空间复杂度：O(n)
*/
func getPermutation(n int, k int) string {
    bitArr := make([]int, n)
    preCountNum := 1
    for i := 0; i < n; i++ {
        bitArr[i] = i + 1
        preCountNum *= i + 1
    }

    k--
    res := ""
    for i := 0; i < n; i++ {
        preCountNum /= (n - i)
        index := k / preCountNum
        res += strconv.Itoa(bitArr[index])
        k = k % preCountNum
        for j := index + 1; j < n; j++ {
            bitArr[j-1] = bitArr[j]
        }
    }
    return res
}
```
