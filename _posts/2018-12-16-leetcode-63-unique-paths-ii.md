---
layout: article
title: 不同路径 II-leetcode
tags: leetcode DP
key: leetcode-63-unique-paths-ii
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/unique-paths-ii/description/)

```go
/**
思路：DP
时间复杂度：O(m*n)
空间复杂度：O(m*n)
*/
func uniquePathsWithObstacles(obstacleGrid [][]int) int {
    m := len(obstacleGrid)
    if m <= 0 {
        return 0
    }
    n := len(obstacleGrid[0])
    if n <= 0 {
        return 0
    }
    grid := initGrid(m, n)
    if 1 == obstacleGrid[0][0] || 1 == obstacleGrid[m-1][n-1] { // 起点和终点有障碍物，则返回0
        return 0
    }
    grid[0][0] = 1
    for i := 0; i < m; i++ {
        for j := 0; j < n; j++ {
            if 1 == obstacleGrid[i][j] { // 当前节点有障碍物，则无法到达
                grid[i][j] = 0
                continue
            }
            if i != 0 {
                grid[i][j] += grid[i-1][j]
            }
            if j != 0 {
                grid[i][j] += grid[i][j-1]
            }
        }
    }
    return grid[m-1][n-1]
}

func initGrid(m int, n int) [][]int {
    grid := make([][]int, m)
    for i := 0; i < m; i++ {
        grid[i] = make([]int, n)
    }
    return grid
}
```
