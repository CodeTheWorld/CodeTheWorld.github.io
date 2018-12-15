---
layout: article
title: 克隆图-leetcode
tags: leetcode queue recursion DFS BFS graph
key: leetcode-133-clone-graph
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/clone-graph/description/)

```go
type UndirectedGraphNode struct {
    Label          int
    Neighbors      []*UndirectedGraphNode
    NeighborsCount int
}

/**
DFS遍历
*/
func DFSCloneGraph(graph *UndirectedGraphNode) *UndirectedGraphNode {
    if nil == graph {
        return nil
    }
    nodeMap := make(map[int]int) // 用于标记是否访问过
    return DFSClone(graph, nodeMap)
}

func DFSClone(graph *UndirectedGraphNode, nodeMap map[int]int) *UndirectedGraphNode {
    if _, exists := nodeMap[graph.Label]; exists { // 访问过，深度遍历到头
        return graph
    }
    // 未访问过，则clone节点
    nodeMap[graph.Label] = graph.Label
    newNode := &UndirectedGraphNode{graph.Label, []*UndirectedGraphNode{}, graph.NeighborsCount}
    for _, node := range graph.Neighbors {
        newNode.Neighbors = append(newNode.Neighbors, DFSClone(node, nodeMap))
    }
    return newNode
}

/**
BFS遍历
*/
func BFSCloneGraph(graph *UndirectedGraphNode) *UndirectedGraphNode {
    if nil == graph {
        return nil
    }
    nodeMap := make(map[int]*UndirectedGraphNode) // 用于标记是否访问过
    queue := []*UndirectedGraphNode{graph} // 队列
    nodeMap[graph.Label] = &UndirectedGraphNode{graph.Label, []*UndirectedGraphNode{}, graph.NeighborsCount} // map[label] = newNode
    for i := 0; i < len(queue); i++ { // 遍历队列
        for _, node := range queue[i].Neighbors {
            childNode, exists := nodeMap[node.Label]
            if !exists { // map中不存在，说明节点未创建
                queue = append(queue, node)
                childNode = &UndirectedGraphNode{node.Label, []*UndirectedGraphNode{}, node.NeighborsCount} // 邻居节点的邻居为空
                nodeMap[node.Label] = childNode
            }
            nodeMap[queue[i].Label].Neighbors = append(nodeMap[queue[i].Label].Neighbors, childNode)
        }
    }
    return nodeMap[graph.Label]
}
```
