---
layout: article
title: 二叉树的中序遍历-leetcode
tags: leetcode binary-tree stack
key: leetcode-94-binary-tree-inorder-traversal
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/description/)

```go
/**
  思路：递归遍历
*/
func inorderTraversal(root *TreeNode) []int {
    res := []int{}
    if nil != root {
        leftRes := inorderTraversal(root.Left)
        rightRes := inorderTraversal(root.Right)
        res = append(leftRes, root.Val)
        res = append(res, rightRes...)
    }
    return res
}
```

```go
/**
  思路：非递归遍历，利用栈来实现
*/

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

func inorderTraversal(root *TreeNode) []int {
    res := []int{}
    myStack := &stack{[]*TreeNode{}, 0}
    for nil != root || myStack.Top != 0 {
        for nil != root {
            push(myStack, root)
            root = root.Left
        }
        root = pop(myStack)
        res = append(res, root.Val)
        root = root.Right
    }
    return res
}
```
