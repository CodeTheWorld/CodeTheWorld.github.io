---
layout: article
title: 最佳买卖股票时机含冷冻期-leetcode
tags: leetcode DP
key: leetcode-309-best-time-to-buy-and-sell-stock-with-cooldown
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/)

```go
/**
思路：DP
*/
func maxProfit(prices []int) int {
    length := len(prices)
    if length <= 1 {
        return 0
    }
    dp := make([]int, 3) // dp[0]:i-2的dp[0];dp[1]:i-1的dp[0];dp[2]:i-1的dp[1]
    dp[0] = 0
    if prices[0] > prices[1] {
        dp[1] = 0
        dp[2] = 0 - prices[1]
    } else {
        dp[1] = prices[1] - prices[0]
        dp[2] = 0 - prices[0]
    }
    max := 0
    if dp[1] > 0 {
        max = dp[1]
    }
    for i := 2; i < length; i++ {
        profit0 := dp[2] + prices[i]
        if profit0 < dp[1] {
            profit0 = dp[1]
        }
        profit1 := dp[0] - prices[i]
        if profit1 < dp[2] {
            profit1 = dp[2]
        }
        if profit0 > max {
            max = profit0
        }
        if profit1 > max {
            max = profit1
        }
        dp[0], dp[1], dp[2] = dp[1], profit0, profit1
    }
    return max
}
```
