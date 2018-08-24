---
layout:     post
title:      leetcode41缺失的第一个正数
subtitle:   leetcode41 First Missing Positive
date:       2018-08-20
author:     BY
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Blog
---


## 前言

别总想着暴力。

## 正文

### 问题来源

本问题来自leetcode上的41题。用go语言做的

### 问题描述

给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

#### 示例 1:
```
输入: [1,2,0]
输出: 3
```
#### 示例 2:
```
输入: [3,4,-1,1]
输出: 2
```
#### 示例 3:
```
输入: [7,8,9,11,12]
输出: 1
``` 
#### 分析：
暴力开空间思想很简单，使用的是bitmap，就不仔细说了
本人写的Go代码如下：  
```
type Bitmap struct {
        words  []uint64
}
func (bitmap *Bitmap) Has(num int) bool {
        word, bit := num/64, uint(num%64)
        return word < len(bitmap.words) && (bitmap.words[word]&(1<<bit)) != 0
}
func (bitmap *Bitmap) Add(num int) {
        if num < 0 {
                return  
        }       
        word, bit := num/64, uint(num%64)
        // 判断num是否已经存在bitmap中
        if bitmap.words[word]&(1<<bit) == 0 {
                bitmap.words[word] |= 1 << bit
        }       
}
func firstMissingPositive(nums []int) int {
        bitmap := &Bitmap{}
        bitmap.words = make([]uint64, 2^25)   
        for _, num := range nums {
                bitmap.Add(num)
        }       
        i := 1; 
        for ; bitmap.Has(i); i++ {}
        return i
}
```  
而网上给的示例代码是，将属于1-n（n为数组的长度）的数字num放在，与其值对应的num-1的数组下标位置上。值得注意的是nums[nums[i]-1] != nums[i]是为了防止无限循环的情况。
```
//go
func firstMissingPositive(nums []int) int {
	for i := 0; i < len(nums); {
		if nums[i] != i+1 && nums[i] > 0 && nums[i] <= len(nums) && nums[nums[i]-1] != nums[i] {
			tmp := nums[nums[i]-1]
			nums[nums[i]-1] = nums[i]
			nums[i] = tmp
		} else {
			i++
		}
	}
	i := 0
	for ; i < len(nums); i++ {
		if i+1 != nums[i] {
			break
		}
	}
	return i + 1
}
//input:[3,4,-1,1],经过第一个for语句处理：[1,4,3,-1]
```
#### 总结：
多思考是否有简单并且高效的解法

## 结语
闲来无事的话，多练习练习，做做题。
