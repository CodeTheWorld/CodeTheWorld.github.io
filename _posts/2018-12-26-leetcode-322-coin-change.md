---
layout: article
title: 零钱兑换-leetcode
tags: leetcode DP
key: leetcode-322-coin-change
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/coin-change/description/)

```go
/**
  思路：DP
 */
func coinChange(coins []int, amount int) int {
    dp := make([]int, amount+1)
    for i := 1; i <= amount; i++ {
        min := -1
        for _, coin := range coins {
            if i-coin < 0 || -1 == dp[i-coin] {
                continue
            }
            if min < 0 || dp[i-coin]+1 < min {
                min = dp[i-coin] + 1
            }
        }
        dp[i] = min
    }
    return dp[amount]
}
```
