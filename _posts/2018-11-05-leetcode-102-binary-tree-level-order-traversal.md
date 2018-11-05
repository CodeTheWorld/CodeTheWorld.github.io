---
layout: article
title: 二叉树的层次遍历-leetcode
tags: leetcode binary-tree queue recursion
key: leetcode-102-binary-tree-level-order-traversal
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/description/)

```go
/**
  思路：利用队列，将每层的节点塞入队列，当出队时，再分别将其左右子节点入队，由此实现层次遍历
  时间复杂度：O(n)
  空间复杂度：O(n)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func levelOrder(root *TreeNode) [][]int {
    res := [][]int{}
    if nil == root {
        return res
    }
    nodeList, length := []*TreeNode{root}, 1 // 初始化队列&队列长度
    for 0 < length {                         // 每个循环代表一层
        level := []int{}              // 每层的结果slice
        for i := 0; i < length; i++ { // 遍历该层已入队的每个节点
            level = append(level, nodeList[i].Val) // 将出队的节点加入到该层的slice中
            if nil != nodeList[i].Left {
                nodeList = append(nodeList, nodeList[i].Left) // 将左节点加入队列
            }
            if nil != nodeList[i].Right {
                nodeList = append(nodeList, nodeList[i].Right) // 将右节点加入队列
            }
        }
        nodeList = nodeList[length:] // 将遍历过的节点从队列中移除
        length = len(nodeList)
        res = append(res, level) // 将该层的结果加入到res中
    }
    return res
}
```

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

func levelOrder(root *TreeNode) [][]int {
    result := [][]int{}
    return levelOrderRecursion(0, root, result)
}

func levelOrderRecursion(depth int, root *TreeNode, result [][]int) [][]int {
    if nil == root {
        return result
    }
    if depth+1 > len(result) {
        result = append(result, []int{})
    }
    result[depth] = append(result[depth], root.Val)
    result = levelOrderRecursion(depth+1, root.Left, result)
    return levelOrderRecursion(depth+1, root.Right, result)
}
```
