---
layout: article
title: 爬楼梯-leetcode
tags: leetcode DP recursion
key: leetcode-70-climbing-stairs
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/climbing-stairs/description/)

```go
/**
思路：DP
时间复杂度：O(n)
空间复杂度：O(n)
*/
func climbStairs(n int) int {
    stairArr := make([]int, n+2)
    length := n + 2
    stairArr[0], stairArr[1] = 0, 1
    for i := 2; i < length; i++ {
        stairArr[i] = stairArr[i-1] + stairArr[i-2]
    }
    return stairArr[length-1]
}
```

```go
/**
思路：递归
时间复杂度：O(n2)
空间复杂度：O(1)
*/
func recurClimbStairs(n int) int {
    if 1 == n || 2 == n {
        return n
    }
    return recurClimbStairs(n-1) + recurClimbStairs(n-2)
}
```
