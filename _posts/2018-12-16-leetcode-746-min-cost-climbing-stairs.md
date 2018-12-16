---
layout: article
title: 使用最小花费爬楼梯-leetcode
tags: leetcode DP
key: leetcode-746-min-cost-climbing-stairs
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/min-cost-climbing-stairs/description/)

```go
/**
思路：DP
时间复杂度：O(n)
空间复杂度：O(n)
*/
func minCostClimbingStairs(cost []int) int {
    length := len(cost)
    minCostArr := make([]int, length)
    for i := 2; i < length; i++ {
        if (minCostArr[i-1] + cost[i-1]) > (minCostArr[i-2] + cost[i-2]) {
            minCostArr[i] = minCostArr[i-2] + cost[i-2]
        } else {
            minCostArr[i] = minCostArr[i-1] + cost[i-1]
        }
    }
    if (minCostArr[length-1] + cost[length-1]) > (minCostArr[length-2] + cost[length-2]) {
        return minCostArr[length-2] + cost[length-2]
    } else {
        return minCostArr[length-1] + cost[length-1]
    }
}
```
