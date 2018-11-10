---
layout: article
title: 从前序与中序遍历序列构造二叉树-leetcode
tags: leetcode binary-tree recursion
key: leetcode-105-construct-binary-tree-from-preorder-and-inorder-traversal
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)

```go
/**
  思路：递归
  时间复杂度：O(n)
  空间复杂度：O(n)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func buildTree(preorder []int, inorder []int) *TreeNode {
    length := len(preorder)
    if 0 == length {
        return nil
    }
    fmt.Println(preorder[0])
    mid := 0
    for i := 0; i < length; i++ {
        if preorder[0] == inorder[i] { // 查找根节点
            mid = i
            break
        }
    }

    return &TreeNode{preorder[0], buildTree(preorder[1:mid+1], inorder[0:mid]), buildTree(preorder[mid+1:length], inorder[mid+1:length])}
}
```
