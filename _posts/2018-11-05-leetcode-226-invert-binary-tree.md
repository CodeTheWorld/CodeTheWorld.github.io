---
layout: article
title: 翻转二叉树-leetcode
tags: leetcode binary-tree recursion stack
key: leetcode-226-invert-binary-tree
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/invert-binary-tree/description/)

```go
/**
  思路：递归
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func invertTree(root *TreeNode) *TreeNode {
    res := root
    if nil != root {
        root.Left, root.Right = root.Right, root.Left
        invertTree(root.Left)
        invertTree(root.Right)
    }
    return res
}
```

```go
/**
  思路：非递归
  时间复杂度：O(n)
  空间复杂度：O(n)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func invertTree(root *TreeNode) *TreeNode {
    res := root
    myStack := &stack{[]*TreeNode{}, 0}
    for nil != root || myStack.Top != 0 {
        for nil != root {
            push(myStack, root)
            root = root.Left
        }
        root = pop(myStack)
        root.Left, root.Right = root.Right, root.Left
        root = root.Left
    }

    return res
}
```
