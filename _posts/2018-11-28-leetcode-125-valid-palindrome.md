---
layout: article
title: 验证回文串-leetcode
tags: leetcode 双指针
key: leetcode-125-valid-palindrome
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/valid-palindrome/description/)

```go
/**
思路：双指针
时间复杂度：O(n)
空间复杂度：O(1)
*/
func isPalindrome(s string) bool {
    length := len(s)
    for left, right := 0, length-1; left < right; {
        for left < right && !isChar(s[left]) {
            left++
        }
        for left < right && !isChar(s[right]) {
            right--
        }
        if left >= right {
            break
        }
        if !equal(s[left], s[right]) {
            return false
        }
        left++
        right--
    }
    return true
}

func isChar(char byte) bool {
    return (char >= 'a' && char <= 'z') || (char >= 'A' && char <= 'Z') || (char >= '0' && char <= '9')
}

func equal(charA byte, charB byte) bool {
    if charA >= 'a' && charA <= 'z' {
        charA = charA + 'A' - 'a'
    }
    if charB >= 'a' && charB <= 'z' {
        charB = charB + 'A' - 'a'
    }
    return charA == charB
}
```
