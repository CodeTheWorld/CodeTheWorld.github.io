---
layout: article
title: 二叉搜索树的范围和-leetcode
tags: leetcode binary-tree binary-search-tree
key: leetcode-938-range-sum-of-bst
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/range-sum-of-bst/description/)

```go
/**
思路：二叉搜索树，找到候选根节点，之后中序遍历
时间复杂度：O(logn + m)
空间复杂度：O(1)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func rangeSumBST(root *TreeNode, L int, R int) int {
    sum := 0
    if nil != root {
        if root.Val >= L {
            sum += rangeSumBST(root.Left, L, R)
        }
        if root.Val >= L && root.Val <= R {
            sum += root.Val
        }
        if root.Val <= R {
            sum += rangeSumBST(root.Right, L, R)
        }
    }
    return sum
}
```
