---
layout:     post
title:      Fisher–Yates洗牌算法
subtitle:   Fisher–Yates shuffle
author:     BY
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Blog
---


## 前言

新的一年，好好学习。

## 正文

### 问题来源

看代码的时候看到该算法。

### 问题描述

给定一个数组，将其完全打乱。 

#### 分析：
1.定义一个数组（shuffled），长度（length）是原数组（arr）长度  
2.取 0 到 index (初始0) 随机值 rand, shuffled[index] = shuffled[rand], shuffled[rand] = arr[index]  
3.index++ ; 重复第二步，直到 index = length -1  
简单来说，就是 shuffled 从 0 到 length-1 的赋值过程，并且新加入的值是 arr[index]。  

go语言版实现(math/rand源码包)
```
func (r *Rand) Shuffle(n int, swap func(i, j int)) {
	if n < 0 {
		panic("invalid argument to Shuffle")
	}
	i := n - 1
	for ; i > 1<<31-1-1; i-- {
		j := int(r.Int63n(int64(i + 1)))
		swap(i, j)
	}
	for ; i > 0; i-- {
		j := int(r.Int31n(int32(i + 1)))
		swap(i, j)
	}
}
```
如何调用
```
var r = rand.New(rand.NewSource(time.Now().UnixNano()))
r.Shuffle(len(nodes), func(i, j int) {
	nodes[i], nodes[j] = nodes[j], nodes[i]
})
```

#### 总结：
勤思考。  

## 结语
不管怎么样好好加油。
