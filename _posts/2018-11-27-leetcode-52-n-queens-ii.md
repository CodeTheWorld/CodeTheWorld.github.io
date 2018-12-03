---
layout: article
title: N皇后 II-leetcode
tags: leetcode 回溯算法
key: leetcode-52-n-queens-ii
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/n-queens-ii/description/)

```go
/**
 思路：回溯
 */
func totalNQueens(n int) int {
    return queen(0, make([]int, n), n)
}

func queen(col int, board []int, n int) int {
    if col == n {
        return 1
    }
    total := 0
    for row := 0; row < n; row++ {
        board[col] = row
        if !canPlace(board, col) {
            continue
        }
        nextCount := queen(col+1, board, n)
        total += nextCount
    }
    return total
}

/**
是否可放置皇后
*/
func canPlace(board []int, col int) bool {
    for i := 0; i < col; i++ {
        if board[i] == board[col] || col-i == board[col]-board[i] || i-col == board[col]-board[i] {
            return false
        }
    }
    return true
}
```
