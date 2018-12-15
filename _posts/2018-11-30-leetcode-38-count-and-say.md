---
layout: article
title: 报数-leetcode
tags: leetcode recursion
key: leetcode-38-count-and-say
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/count-and-say/description/)

```go
/**
思路：递归
*/
func countAndSay(n int) string {
    if 1 == n {
        return "1"
    }
    str := countAndSay(n - 1)
    lastChar := str[0]
    count := 1
    res := []byte{}
    for i := 1; i < len(str); i++ {
        if str[i] == lastChar {
            count++
        } else {
            res = append(res, byte('0')+byte(count), lastChar)
            count = 1
            lastChar = str[i]
        }
    }
    return string(append(res, byte('0')+byte(count), lastChar))
}
```
