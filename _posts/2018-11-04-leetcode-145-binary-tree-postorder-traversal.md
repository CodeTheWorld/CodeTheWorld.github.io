---
layout: article
title: 二叉树的后序遍历-leetcode
tags: leetcode binary-tree stack recursion
key: leetcode-145-binary-tree-postorder-traversal
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/description/)

```go
/**
  思路：递归
*/
func postorderTraversal(root *TreeNode) []int {
    res := []int{}
    if nil != root {
        leftRes := postorderTraversal(root.Left)
        res = append(res, leftRes...)
        rightRes := postorderTraversal(root.Right)
        res = append(res, rightRes...)
        res = append(res, root.Val)
    }
    return res
}
```

```go
/**
  思路：非递归遍历，为避免死循环的出现，记录了上次访问的节点
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

func postorderTraversal(root *TreeNode) []int {
    res := []int{}
    myStack := &stack{[]*TreeNode{}, 0}
    var lastVisit *TreeNode  // 上次访问的节点

    for nil != root || 0 != myStack.Top {
        for nil != root {  // dfs
            push(myStack, root)
            root = root.Left
        }
        root = pop(myStack)
        if nil == root.Right || lastVisit == root.Right {  // 因父节点紧跟在右侧子节点之后访问，故用这种方式表示该子树的右侧子树已遍历完成
            res = append(res, root.Val)
            lastVisit = root
            root = nil
        } else {
            push(myStack, root)
            root = root.Right
        }
    }
    return res
}
```
