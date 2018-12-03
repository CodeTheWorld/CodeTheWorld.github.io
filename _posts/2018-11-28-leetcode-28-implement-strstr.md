---
layout: article
title: 实现strStr()-leetcode
tags: leetcode
key: leetcode-28-implement-strstr
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/implement-strstr/description/)

```go
/**
 思路：利用i,j分别表示haystack的起始index和needle遍历的位置
 */
func strStr(haystack string, needle string) int {
    needleLength := len(needle)
    haystackLength := len(haystack)
    if 0 == needleLength {
        return 0
    }
    index := -1
    for i := 0; i < haystackLength; i++ {
        if (haystackLength - i) < needleLength {
            return index
        }
        j := 0
        for ; j < needleLength && (i+j) < haystackLength; j++ {
            if haystack[i+j] != needle[j] {
                j = 0
                break
            }
        }
        if j == needleLength {
            index = i
            break
        }
    }
    return index
}
```
