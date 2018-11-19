---
layout: article
title: 二叉树的右视图-leetcode
tags: leetcode binary-tree queue
key: leetcode-199-binary-tree-right-side-view
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/binary-tree-right-side-view/description/)

```go
/**
思路：类似层次遍历
时间复杂度：O(n)
空间复杂度：O(n)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func rightSideView(root *TreeNode) []int {
    res := []int{}
    if nil == root {
        return res
    }
    queue := []*TreeNode{root}
    length := 1
    for i := 0; 0 != length; i++ {
        res = append(res, queue[length-1].Val)
        for j := 0; j < length; j++ {
            if nil != queue[j].Left {
                queue = append(queue, queue[j].Left)
            }
            if nil != queue[j].Right {
                queue = append(queue, queue[j].Right)
            }
        }
        queue = queue[length:]
        length = len(queue)
    }
    return res
}
```
