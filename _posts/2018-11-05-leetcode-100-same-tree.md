---
layout: article
title: 相同的树-leetcode
tags: leetcode binary-tree
key: leetcode-100-same-tree
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/same-tree/description/)

```go
/**
  思路：递归
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
func isSameTree(p *TreeNode, q *TreeNode) bool {
    if nil == p && nil == q {
        return true
    }
    if nil == p || nil == q || p.Val != q.Val {
        return false
    }
    leftRes := isSameTree(p.Left, q.Left)
    rightRes := isSameTree(p.Right, q.Right)
    return leftRes && rightRes
}
```
