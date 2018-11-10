---
layout: article
title: 二叉树的最大深度-leetcode
tags: leetcode binary-tree queue recursion
key: leetcode-104-maximum-depth-of-binary-tree
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/description/)

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

func maxDepth(root *TreeNode) int {
    if nil == root {
        return 0
    }
    leftDepth := maxDepth(root.Left)
    rightDepth := maxDepth(root.Right)
    if leftDepth > rightDepth {
        return leftDepth + 1
    } else {
        return rightDepth + 1
    }
}
```

```go
/**
  思路：利用队列，迭代
  时间复杂度：O(n)
  空间复杂度：O(n)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func maxDepth(root *TreeNode) int {
    depth := 0
    queue := []*TreeNode{root}
    length := len(queue)

    for length > 0 {
        for i := 0; i < length; i++ {
            if nil == queue[i] {
                continue
            }
            queue = append(queue, queue[i].Left)
            queue = append(queue, queue[i].Right)
        }
        queue = queue[length:]
        length = len(queue)
        if length > 0 {
            depth++
        }
    }
    return depth
}
```
