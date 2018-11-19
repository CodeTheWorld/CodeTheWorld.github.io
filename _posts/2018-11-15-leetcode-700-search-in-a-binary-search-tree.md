---
layout: article
title: 二叉搜索树中的搜索-leetcode
tags: leetcode binary-search-tree binary-tree
key: leetcode-700-search-in-a-binary-search-tree
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/search-in-a-binary-search-tree/description/)

```go
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func searchBST(root *TreeNode, val int) *TreeNode {
    if nil == root {
        return nil
    }
    if root.Val == val {
        return root
    } else if root.Val > val {
        return searchBST(root.Left, val)
    } else {
        return searchBST(root.Right, val)
    }
}
```
