---
layout: article
title: 不同路径-leetcode
tags: leetcode DP
key: leetcode-62-unique-paths
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/unique-paths/description/)

```go
/**
思路：DP
时间复杂度：O(m*n)
空间复杂度：O(m*n)
*/
func uniquePaths(m int, n int) int {
    if m <= 0 || n <= 0 {
        return 0
    }
    board := initBoard(m, n) // board中的每格表示到达该格的路径个数
    board[0][0] = 1
    for i := 0; i < n; i++ {
        for j := 0; j < m; j++ { // 每格的路径数=上面一格的路径数+左边一格的路径数
            if 0 != j {
                board[i][j] += board[i][j-1]
            }
            if 0 != i {
                board[i][j] += board[i-1][j]
            }
        }
    }
    return board[n-1][m-1]
}

/**
初始化二维数组
*/
func initBoard(m int, n int) [][]int {
    board := make([][]int, n)
    for i := 0; i < n; i++ {
        board[i] = make([]int, m)
    }
    return board
}
```
