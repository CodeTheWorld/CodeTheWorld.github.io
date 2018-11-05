---
layout: article
title: 二叉树的层次遍历 II-leetcode
tags: leetcode binary-tree recursion queue
key: leetcode-107-binary-tree-level-order-traversal-ii
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/description/)

```go
/**
  思路：利用队列，层次遍历，将每层的结果slice插到结果集第一个
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func levelOrderBottom(root *TreeNode) [][]int {
    result := [][]int{}
    if nil == root {
        return result
    }
    queue := []*TreeNode{root}
    length := len(queue)
    for 0 < length {
        level := []int{}
        for i := 0; i < length; i++ {
            level = append(level, queue[i].Val)
            if nil != queue[i].Left {
                queue = append(queue, queue[i].Left)
            }
            if nil != queue[i].Right {
                queue = append(queue, queue[i].Right)
            }
        }
        queue = queue[length:]
        length = len(queue)
        result = append([][]int{level}, result...)
    }
    return result
}
```

```go
/**
  思路：递归层次遍历，然后翻转slice
  时间复杂度：O(n)
  空间复杂度：O(1)
*/
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func levelOrderBottom1(root *TreeNode) [][]int {
    result := [][]int{}
    result = levelOrderBottomRecursion(0, root, result) // 递归遍历
    // 翻转slice
    length := len(result)
    for i, j := 0, length-1; i < j; i, j = i+1, j-1 {
        result[i], result[j] = result[j], result[i]
    }
    return result
}

func levelOrderBottomRecursion(depth int, root *TreeNode, result [][]int) [][]int {
    if nil == root {
        return result
    }
    if depth+1 > len(result) { // 如果depth层slice还未初始化，则初始化
        result = append(result, []int{})
    }
    result[depth] = append(result[depth], root.Val)                // 将节点加入对应层
    result = levelOrderBottomRecursion(depth+1, root.Left, result) // 递归处理下一层的左节点
    return levelOrderBottomRecursion(depth+1, root.Right, result)  // 递归处理下一层的右节点
}
```
