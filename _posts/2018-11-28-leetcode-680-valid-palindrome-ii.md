---
layout: article
title: 验证回文字符串 Ⅱ-leetcode
tags: leetcode 双指针
key: leetcode-680-valid-palindrome-ii
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/valid-palindrome-ii/description/)


```go
/**
思路：双指针
时间复杂度：O(n)
空间复杂度：O(1)
*/
func validPalindrome(s string) bool {
    length := len(s)
    isDelete := false
    try := false
    var leftIndex, rightIndex int
    for left, right := 0, length-1; left < right; {
        if s[left] == s[right] {
            left++
            right--
            continue
        }
        if !isDelete {
            leftIndex = left
            rightIndex = right
            isDelete = true
            left++
        } else if try {
            return false
        } else {
            left = leftIndex
            right = rightIndex
            right--
            try = true
        }
    }
    return true
}
```
