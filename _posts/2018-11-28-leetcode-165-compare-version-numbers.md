---
layout: article
title: 比较版本号-leetcode
tags: leetcode
key: leetcode-165-compare-version-numbers
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/compare-version-numbers/description/)

```go
func compareVersion(version1 string, version2 string) int {
    length1, length2 := len(version1), len(version2)
    i, j := 0, 0
    int1, int2 := 0, 0
    for i < length1 || j < length2 {
        for i < length1 && version1[i] != '.' {
            int1 = int1*10 + int(version1[i]-'0')
            i++
        }
        for j < length2 && version2[j] != '.' {
            int2 = int2*10 + int(version2[j]-'0')
            j++
        }
        if int1 > int2 {
            return 1
        } else if int1 < int2 {
            return -1
        } else {
            int1, int2 = 0, 0
            i++
            j++
        }
    }
    return 0
}
```
