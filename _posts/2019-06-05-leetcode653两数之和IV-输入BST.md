---
layout:     post
title:      leetcode653两数之和IV-输入BST
subtitle:   leetcode653 Two Sum IV - Input is a BST
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

本问题来自leetcode上的653题。

### 问题描述

给定一个二叉搜索树和一个目标结果，如果 BST 中存在两个元素且它们的和等于给定的目标结果，则返回 true。  

#### 示例 1：
```
输入: 
    5
   / \
  3   6
 / \   \
2   4   7
Target = 9
输出: True
```

#### 示例 2：
```
输入: 
    5
   / \
  3   6
 / \   \
2   4   7
Target = 28
输出: False
```

#### 分析：
```
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
var m map[int]bool
func findTarget(root *TreeNode, k int) bool {
    m = make(map[int]bool)
    return dfs(root, k)
}

func dfs(root *TreeNode, k int) bool {
    if root == nil {
        return false
    }
    n := root.Val
    if _, ok := m[k-n]; ok {
        return true
    }
    m[n] = true
    return dfs(root.Left, k) || dfs(root.Right, k)
}
```
```
func findTarget(root *TreeNode, k int) bool {
        res := false
    arr := []int{}
    midleOrder(root,&arr)
    p := 0
    q := len(arr) -1 
    for p != q{
        if arr[p] + arr[q] == k {
            res = true
            break
        }
        if arr[p] + arr[q] > k{
            q--
            continue
        }
        if arr[p] + arr[q] < k{
            p++
            continue
        }
    }
    return res
}

func midleOrder(root *TreeNode, arr *[]int) {
    if root == nil {
        return
    }
    midleOrder(root.Left, arr)
    *arr = append(*arr, root.Val)
    midleOrder(root.Right, arr)
}
```


#### 总结：
勤思考。  

## 结语
不管怎么样好好加油。
