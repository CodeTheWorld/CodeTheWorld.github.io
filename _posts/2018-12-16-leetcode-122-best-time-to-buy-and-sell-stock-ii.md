---
layout: article
title: 买卖股票的最佳时机 II-leetcode
tags: leetcode DP
key: leetcode-122-best-time-to-buy-and-sell-stock-ii
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

```go
/**
思路：DP
*/
func maxProfit(prices []int) int {
    length := len(prices)
    if length <= 0 {
        return 0
    }
    dp := make([]int, 2)
    dp[0], dp[1] = 0, 0-prices[0]
    max := 0
    for i := 1; i < length; i++ {
        profit0 := dp[1] + prices[i]
        if profit0 < dp[0] {
            profit0 = dp[0]
        }
        profit1 := dp[0] - prices[i]
        if profit1 < dp[1] {
            profit1 = dp[1]
        }
        if profit0 > profit1 {
            max = profit0
        } else {
            max = profit1
        }
        dp[0], dp[1] = profit0, profit1
    }
    return max
}
```
