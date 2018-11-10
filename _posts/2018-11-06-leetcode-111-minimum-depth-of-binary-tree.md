---
layout: article
title: 二叉树的最小深度-leetcode
tags: leetcode binary-tree queue recursion
key: leetcode-111-minimum-depth-of-binary-tree
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/description/)

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

func minDepth(root *TreeNode) int {
    if nil == root {
        return 0
    }
    left := minDepth(root.Left)   // 左子树递归
    right := minDepth(root.Right) // 右子树递归
    if 0 == left {                // 左子树为空，向右延伸
        return right + 1
    } else if 0 == right { // 右子树为空，向左延伸
        return left + 1
    } else { // 左右子树都不为空，向高度小的延伸
        if left < right {
            return left + 1
        } else {
            return right + 1
        }
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

func minDepth(root *TreeNode) int {
    depth := 0
    queue := []*TreeNode{root}
    length := len(queue)

    for length > 0 {
        for i := 0; i < length; i++ {
            if nil == queue[i] {
                continue
            }
            if nil == queue[i].Left && nil == queue[i].Right {
                return depth + 1
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
