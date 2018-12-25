---
layout: article
title: 另一个树的子树-leetcode
tags: leetcode binary-tree
key: leetcode-572-subtree-of-another-tree
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/subtree-of-another-tree/description/)

```go
/**
思路：遍历s树，所有子树和树t比较是否相同的树
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func isSubtree(s *TreeNode, t *TreeNode) bool {
    if isSameTree(s, t) {
        return true
    }
    if nil == s {
        return false
    }
    return isSubtree(s.Left, t) || isSubtree(s.Right, t)
}

func isSameTree(s *TreeNode, t *TreeNode) bool {
    if nil == s && nil == t {
        return true
    }
    if nil != s && nil != t && s.Val == t.Val {
        return isSameTree(s.Left, t.Left) && isSameTree(s.Right, t.Right)
    }
    return false
}
```
