---
layout: article
title: 从中序与后序遍历序列构造二叉树-leetcode
tags: leetcode binary-tree recursion
key: leetcode-106-construct-binary-tree-from-inorder-and-postorder-traversal
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)

```go
/**
思路：递归
时间复杂度：O(n*log(n))
空间复杂度：O(n)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func buildTree(inorder []int, postorder []int) *TreeNode {
    length := len(inorder)
    if 0 == length {
        return nil
    }
    mid := 0
    for i := 0; i < length; i++ {
        if inorder[i] == postorder[length-1] {
            mid = i
            break
        }
    }
    fmt.Println(postorder[length-1])

    return &TreeNode{postorder[length-1], buildTree(inorder[0:mid], postorder[0:mid]), buildTree(inorder[mid+1:length], postorder[mid:length-1])}
}
```
