---
layout: article
title: N皇后-leetcode
tags: leetcode 回溯算法 递归
key: leetcode-51-n-queens
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/n-queens/description/)

```go
/**
思路：回溯算法，递归实现
*/
func solveNQueens(n int) [][]string {
    board := make([]int, n)
    situations := queen(0, board, n)
    res := [][]string{}
    for _, situation := range situations {
        res = append(res, convert(situation, n))
    }
    return res
}

func convert(nums []int, n int) []string {
    res := make([]string, n)
    for i, v := range nums {
        str := ""
        for j := 0; j < n; j++ {
            if j == v {
                str += "Q"
            } else {
                str += "."
            }
        }
        res[i] = str
    }
    return res
}

func queen(col int, board []int, n int) [][]int {
    if col == n {
        return [][]int{board}
    }
    res := [][]int{}
    for row := 0; row < n; row++ {
        board[col] = row
        if !canPlace(board, col) {
            continue
        }
        nextSit := queen(col+1, board, n)
        if 0 < len(nextSit) {
            for _, item := range nextSit {
                tmp := make([]int, n)
                copy(tmp, item)
                res = append(res, tmp)
            }
        }
    }
    return res
}

func convert(nums []int, n int) []string {
    res := make([]string, n)
    for i, v := range nums {
        str := ""
        for j := 0; j < n; j++ {
            if j == v {
                str += "Q"
            } else {
                str += "."
            }
        }
        res[i] = str
    }
    return res
}

func queen(col int, board []int, n int) [][]int {
    if col == n {
        return [][]int{board}
    }
    res := [][]int{}
    for row := 0; row < n; row++ {
        board[col] = row
        if !canPlace(board, col) {
            continue
        }
        nextSit := queen(col+1, board, n)
        if 0 < len(nextSit) {
            for _, item := range nextSit {
                tmp := make([]int, n)
                copy(tmp, item)
                res = append(res, tmp)
            }
        }
    }
    return res
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

```go
/**
思路：全排列
*/
func solveNQueens(n int) [][]string {
    queens := make([]int, n)
    for i := 0; i < n; i++ {
        queens[i] = i
    }
    permutations := permute(queens, 0)
    res := [][]string{}
    for _, items := range permutations {
        ok := check(items, n)
        if ok {
            res = append(res, convert(items, n))
        }
    }
    return res
}

func convert(nums []int, n int) []string {
    res := make([]string, n)
    for i, v := range nums {
        str := ""
        for j := 0; j < n; j++ {
            if j == v {
                str += "Q"
            } else {
                str += "."
            }
        }
        res[i] = str
    }
    return res
}

func check(nums []int, n int) bool {
    for i := 0; i < n; i++ {
        for j := i + 1; j < n; j++ {
            if (j-i == nums[j]-nums[i]) || (i-j == nums[j]-nums[i]) {
                return false
            }
        }
    }
    return true
}

func permute(nums []int, index int) [][]int {
    length := len(nums)
    res := [][]int{}
    if index == length {
        return res
    }
    for i := index; i < length; i++ {
        nums[i], nums[index] = nums[index], nums[i]
        nextRes := permute(nums, index+1)
        nextLength := len(nextRes)
        if 0 == nextLength {
            res = append(res, []int{nums[index]})
        } else {
            for _, items := range nextRes {
                res = append(res, append(items, nums[index]))
            }
        }
        nums[i], nums[index] = nums[index], nums[i]
    }
    return res
}
```
