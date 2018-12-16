---
layout: article
title: 买卖股票的最佳时机-leetcode
tags: leetcode
key: leetcode-121-best-time-to-buy-and-sell-stock
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/description/)

```go
func maxProfit(prices []int) int {
    length := len(prices)
    if length <= 0 {
        return 0
    }
    minPrice, max := prices[0], 0
    for i := 1; i < length; i++ {
        if prices[i] < minPrice {
            minPrice = prices[i]
            continue
        }
        if prices[i]-minPrice > max {
            max = prices[i] - minPrice
        }
    }
    return max
}
```
