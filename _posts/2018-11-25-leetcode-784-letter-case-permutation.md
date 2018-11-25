---
layout: article
title: 字母大小写全排列-leetcode
tags: leetcode
key: leetcode-784-letter-case-permutation
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/letter-case-permutation/description/)

```go
/**
时间复杂度：O(n2)
空间复杂度：O(n)
*/
func letterCasePermutation(S string) []string {
    length := len(S)
    res := []string{""}
    if 0 == length {
        return res
    }
    var strings []string
    for i := 0; i < length; i++ {
        strings = convert(S[i])
        tmpRes := []string{}
        for _, oldStr := range res {
            for _, newStr := range strings {
                tmpRes = append(tmpRes, oldStr+newStr)
            }
        }
        res = tmpRes
    }
    return res
}

func convert(c byte) []string {
    res := []string{}
    if c >= 'a' && c <= 'z' {
        res = append(res, string(c), string(c-'a'+'A'))
    } else if c >= 'A' && c <= 'Z' {
        res = append(res, string(c), string(c-'A'+'a'))
    } else {
        res = append(res, string(c))
    }
    return res
}
```
