---
layout:     post
title:      leetcode168Excel表列名称
subtitle:   leetcode168 Excel Sheet Column Title
author:     BY
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Blog
---


## 前言

新的一年，好好学习。尝试用python写写代码。

## 正文

### 问题来源

本问题来自leetcode上的168题。

### 问题描述

给定一个正整数，返回它在 Excel 表中相对应的列名称。
例如，
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB  
```

#### 示例 1:
```
输入: 701
输出: "ZY"
``` 

#### 分析：
就是转26进制。
```
class Solution(object):
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        stack = []
        while n:
            t = (n + 25) % 26
            stack.append(chr(65 + t))
            n = int(n / 26)
        l = len(stack) - 1
        s = ""
        while l >= 0:
            s += stack[l]
            l = l - 1
        return s
```

别人写的
```
from string import ascii_uppercase

class Solution(object):
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        ret = ""
        lst = list()
        dct = dict(enumerate(ascii_uppercase, start=1))
        # 十进制转为二十六进制
        while n != 0:
            mod = n % 26
            n = n // 26
            if mod == 0:
                mod = 26
                n -= 1
            lst.append(mod)
        return "".join(dct[i] for i in reversed(lst))
```

#### 总结：
勤思考。  
//符号代表取整除 - 返回商的整数部分（向下取整）  
for语句语法糖

## 结语
不管怎么样好好加油。
