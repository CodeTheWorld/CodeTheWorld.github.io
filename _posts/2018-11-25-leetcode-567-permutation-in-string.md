---
layout: article
title: 字符串的排列-leetcode
tags: leetcode 滑动窗口
key: leetcode-567-permutation-in-string
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/permutation-in-string/description/)

```go
/**
思路：滑动窗口
*/
func checkInclusion(s1 string, s2 string) bool {
    length1 := len(s1)
    length2 := len(s2)
    if length1 > length2 {
        return false
    }
    charArr1 := make([]int, 26)
    charArr2 := make([]int, 26)
    for index, char := range s1 {
        charArr1[char-'a']++
        charArr2[s2[index]-'a']++
    }
    if true == isEqual(charArr1, charArr2) {
        return true
    }

    for i := length1; i < length2; i++ {
        charArr2[s2[i]-'a']++
        charArr2[s2[i-length1]-'a']--
        if true == isEqual(charArr1, charArr2) {
            return true
        }
    }
    return false
}

func isEqual(slice1 []int, slice2 []int) bool {
    len1 := len(slice1)
    len2 := len(slice2)
    if len1 != len2 {
        return false
    }
    for i := 0; i < len1; i++ {
        if slice1[i] != slice2[i] {
            return false
        }
    }
    return true
}
```
