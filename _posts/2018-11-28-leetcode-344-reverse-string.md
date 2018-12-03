---
layout: article
title: 反转字符串-leetcode
tags: leetcode
key: leetcode-344-reverse-string
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/reverse-string/description/)

```go
func reverseString(s string) string {
    length := len(s)
    newStr := make([]byte, length)
    for i := 0; i < length; i++ {
        newStr[length-i-1] = s[i]
    }
    return string(newStr)
}
```
