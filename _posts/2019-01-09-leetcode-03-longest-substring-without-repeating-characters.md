---
layout: article
title: 无重复字符的最长子串-leetcode
tags: leetcode
key: leetcode-03-longest-substring-without-repeating-characters
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/description/)

```go
/**
 * 思路：滑动窗口
 * 如果该字符不存在于子串，则遍历下一个
 * 否则，计算子串最大长度，同时移动子串起始位置
 */
func lengthOfLongestSubstring(s string) int {
    length := len(s)
    if length <= 1 {
        return length
    }
    charArr := make([]int, 128)   // ASCII字符map，key为字符，val为该字符上次在该串中出现的位置
    start, end, maxLen := 1, 1, 0 // 将字符串s虚拟为“ s”，即从1下标开始，为了便于统一处理start
    for end <= length {           // 遍历
        if start <= charArr[s[end-1]] { // 字符是否出现在start之后，是的话，则start和end下标对应的字符是相同的
            tmpLen := end - start
            if tmpLen > maxLen {
                maxLen = tmpLen
            }
            start = charArr[s[end-1]] + 1 // start跳跃
        }
        charArr[s[end-1]] = end
        end++
    }
    lastLen := length - start + 1 // 计算最后一个子串的长度
    if lastLen > maxLen {
        maxLen = lastLen
    }
    return maxLen
}
```
