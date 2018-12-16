---
layout: article
title: 买卖股票的最佳时机含手续费-leetcode
tags: leetcode DP
key: leetcode-714-best-time-to-buy-and-sell-stock-with-transaction-fee
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/description/)

```go
/**
思路：DP
时间复杂度：O(n)
空间复杂度：O(1)
*/
func maxProfit(prices []int, fee int) int {
    length := len(prices)
    dp := make([]int, 2)
    dp[0], dp[1] = 0, 0-prices[0]
    max := 0
    for i := 1; i < length; i++ {
        profit0 := dp[1] + prices[i] - fee
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
