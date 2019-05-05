---
layout:     post
title:      leetcode28 实现strStr
subtitle:   leetcode28 Implement strStr
date:       2019-01-04
author:     BY
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Blog
---


## 前言

虽然可以暴力，但是要知道高效的方法

## 正文

### 问题来源

本问题来自leetcode上的28题。  
### 问题描述

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

##### 示例 1
```
输入: haystack = "hello", needle = "ll"
输出: 2
```  

##### 示例 2
```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```  

#### 分析：
官方给出的算法实现。“你怎么穿上品如的衣服了”  
```
func strStr(haystack string, needle string) int {
    if needle == ""{
        return 0
    }else if len(haystack) < len(needle) {
        return -1
    }
    for i:=0;i<len(haystack)-len(needle)+1;i++{
        if needle == haystack[i:len(needle)+i]{
            return i
        }
    }
    return -1
}
```
很自然的想到KMP算法。KMP算法很好理解，但是写的过程历经各种坑  
```
func next(needle string) []int {
    l := len(needle)
    ret := make([]int, l+1)
    ret[0], ret[1] = -1, 0
    k := 0
    for j := 1; j < l - 1;  {
        if (k==-1)||(needle[j] == needle[k]) {
            k++
            j++
            ret[j] = k
        } else {
            k = ret[k]
        }
    }
    return ret
}
func strStr(haystack string, needle string) int {
    if "" == needle {
        return 0
    }
    l := len(haystack)
    n := next(needle)
    nl := len(needle)
    i := 0
    k := 0
    for (i < l)&&(k<nl) {
        if (k==-1)||(haystack[i] == needle[k]) {
            k++
            i++
        } else {            
            k = n[k]
        }
    }
    if k == nl {
        return i - k
    }
    //fmt.Println(haystack,next(needle))
    return -1
}
```
#### 总结：
glibc 2.9 之后的 strstr() 在一定情况下会用高效的 [Two Way algorithm](http://www-igm.univ-mlv.fr/~lecroq/string/node26.html)，之前的版本是普通的二重循环查找，因此用不着自己写。  这段话网上抄来的
## 结语
不要懒，多看多写。
