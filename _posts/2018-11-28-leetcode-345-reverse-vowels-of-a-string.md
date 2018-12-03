---
layout: article
title: 反转字符串中的元音字母-leetcode
tags: leetcode
key: leetcode-345-reverse-vowels-of-a-string
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/description/)

```go
func reverseVowels(s string) string {
    length := len(s)
    res := make([]byte, length)
    for i, j := 0, length-1; i <= j; {
        for i <= j && !isVowel(s[i]) {
            res[i] = s[i]
            i++
            continue
        }
        for i <= j && !isVowel(s[j]) {
            res[j] = s[j]
            j--
            continue
        }
        if i <= j {
            res[i], res[j] = s[j], s[i]
            i++
            j--
        }
    }
    return string(res)
}

func isVowel(char byte) bool {
    res := false
    switch char {
    case 'a':
        fallthrough
    case 'e':
        fallthrough
    case 'i':
        fallthrough
    case 'o':
        fallthrough
    case 'u':
        fallthrough
    case 'A':
        fallthrough
    case 'E':
        fallthrough
    case 'I':
        fallthrough
    case 'O':
        fallthrough
    case 'U':
        res = true
        break
    default:
    }
    return res
}
```
