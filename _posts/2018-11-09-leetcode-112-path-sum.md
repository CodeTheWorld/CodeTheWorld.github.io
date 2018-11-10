---
layout: article
title: 路径总和-leetcode
tags: leetcode binary-tree recursion
key: leetcode-112-path-sum
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/path-sum/description/)

```go
/**
  思路：遍历，递减
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func hasPathSum(root *TreeNode, sum int) bool {
    if nil == root {
        return false
    }
    sum -= root.Val
    if nil == root.Left && nil == root.Right {
        return 0 == sum
    }
    res := false
    if nil != root.Left {
        leftRes := hasPathSum(root.Left, sum)
        res = res || leftRes
    }
    if nil != root.Right {
        rightRes := hasPathSum(root.Right, sum)
        res = res || rightRes
    }
    return res
}
```
