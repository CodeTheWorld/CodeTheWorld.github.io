---
layout: article
title: 位1的个数-leetcode
tags: leetcode hammingweight
key: leetcode-191-number-of-1-bits
mathajx: false
---

<!--more-->

[题目链接](https://leetcode-cn.com/problems/number-of-1-bits/submissions/)

```go
/**
 * 思路：十进制转二进制
 */
func hammingWeight(num uint32) int {
	count := 0
	for ;num > 0; num = num / 2 {
		count += int(num % 2)
	}
	return count
}
```

```go
/**
 * 思路：位与
 */
func hammingWeight(num uint32) int {
	count := 0
	mask := uint32(1)
	for i := 0; i < 32; i++ {
		if mask&num != 0 {
			count++
		}
		mask <<= 1
	}
	return count
}
```

```go
/**
 * 思路：n&(n-1) = 0
 */
func hammingWeight(num uint32) int {
	count := 0
	for num != 0 {
		num = num & (num-1)
		count++
	}
	return count
}
```
