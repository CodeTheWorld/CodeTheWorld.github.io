---
layout: article
title: 二叉树的前序遍历-leetcode
tags: leetcode binary-tree stack recursion
key: leetcode-144-binary-tree-preorder-traversal
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/description/)

```go
/**
  思路：递归
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func preorderTraversal(root *TreeNode) []int {
    res := []int{}
    if nil != root {
        res = append(res, root.Val)
        leftRes := preorderTraversal(root.Left)
        res = append(res, leftRes...)
        rightRes := preorderTraversal(root.Right)
        res = append(res, rightRes...)
    }
    return res
}
```

```go
/**
  思路：非递归，利用栈实现
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

type stack struct {
    BinTree []*TreeNode
    Top     int
}

func push(nodeStack *stack, node *TreeNode) {
    nodeStack.BinTree = append(nodeStack.BinTree, node)
    nodeStack.Top++
}

func pop(nodeStack *stack) *TreeNode {
    var res *TreeNode
    nodeStack.Top--
    if nodeStack.Top < 0 {
        res = nil
    } else {
        res = nodeStack.BinTree[nodeStack.Top]
    }
    nodeStack.BinTree = nodeStack.BinTree[:nodeStack.Top]
    return res
}

func preorderTraversal(root *TreeNode) []int {
    res := []int{}
    myStack := &stack{[]*TreeNode{}, 0}
    for nil != root || 0 != myStack.Top {
        for nil != root {
            res = append(res, root.Val)
            push(myStack, root.Right)
            root = root.Left
        }
        root = pop(myStack)
    }
    return res
}
```
