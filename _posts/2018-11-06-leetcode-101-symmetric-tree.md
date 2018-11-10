---
layout: article
title: 对称二叉树-leetcode
tags: leetcode binary-tree stack recursion
key: leetcode-101-symmetric-tree
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/symmetric-tree/description/)

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

func isSymmetric(root *TreeNode) bool {
    if nil == root {
        return true
    }
    return isSymmetricRecursion(root.Left, root.Right)
}

func isSymmetricRecursion(left *TreeNode, right *TreeNode) bool {
    if nil == left && nil == right {
        return true
    }
    if nil == left || nil == right || left.Val != right.Val {
        return false
    }
    outterRes := isSymmetricRecursion(left.Left, right.Right)
    innerRes := isSymmetricRecursion(left.Right, right.Left)
    return outterRes && innerRes
}
```

```go
/**
  思路：利用栈，迭代
  时间复杂度：O(n)
  空间复杂度：O(n)
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

func isSymmetric(root *TreeNode) bool {
    if nil == root {
        return true
    }
    myStack := &stack{[]*TreeNode{}, 0}
    // 左右子节点都压栈
    push(myStack, root.Left)
    push(myStack, root.Right)

    for 0 < myStack.Top {
        left := pop(myStack)
        right := pop(myStack)
        if nil == left && nil == right {
            continue
        }
        if nil == left || nil == right || left.Val != right.Val {
            return false
        }
        push(myStack, left.Left)
        push(myStack, right.Right)
        push(myStack, left.Right)
        push(myStack, right.Left)
    }
    return true
}
```
