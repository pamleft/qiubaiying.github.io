---
layout:     post
title:      leetcode208实现Trie(前缀树)
subtitle:   leetcode208 Implement Trie (Prefix Tree)
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

本问题来自leetcode上的208题。

### 问题描述

实现一个 Trie (前缀树)，包含 insert, search, 和 startsWith 这三个操作。  

#### 示例 ：
```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true
```

#### 分析：
```
type Trie struct {
    isEnd bool
	son []*Trie
}


/** Initialize your data structure here. */
func Constructor() Trie {
    var t Trie
	t.son = make([]*Trie, 26)
	return t
}


/** Inserts a word into the trie. */
func (this *Trie) Insert(word string)  {
	t := this
	for i := 0; i < len(word); i++ {
		if nil == t.son[word[i] - 'a'] {
			temp := Constructor()
			t.son[word[i]-'a'] = &temp
		} 
		t = t.son[word[i]-'a']
	}
	t.isEnd = true
}


/** Returns if the word is in the trie. */
func (this *Trie) Search(word string) bool {
    t := this
	for i := 0; i < len(word); i++ {
		if nil == t.son[word[i] - 'a'] {
			return false
		} 
		t = t.son[word[i]-'a']
	}
	return t.isEnd
}


/** Returns if there is any word in the trie that starts with the given prefix. */
func (this *Trie) StartsWith(prefix string) bool {
    t := this
	for i := 0; i < len(prefix); i++ {
		if nil == t.son[prefix[i] - 'a'] {
			return false
		} 
		t = t.son[prefix[i]-'a']
	}
	return true
}
```
C++版本
```
#include<iostream>
#include<cstring>
using namespace std;
const int branchNum = 26;

struct TrieNode
{
	bool isStr;
	TrieNode *next[branchNum];
};

void Insert(TrieNode *root, const char *word);
bool Search(TrieNode *root, const char *word);
void Delete(TrieNode *node);

int main() {
	TrieNode *root=new TrieNode();
	root->isStr=false;
	memset(root->next, NULL, sizeof(root->next));
	Insert(root, "a");
	Insert(root, "bcd");
	Insert(root, "xyz");
	Insert(root, "abcdef");
	if (Search(root, "a")) {
		cout << "a exist" << endl;
	}
	Delete(root);
	return 0;
}

void Insert(TrieNode *root, const char *word) {
	TrieNode *location = root;
	while (*word) {
		if (location->next[*word-'a'] == NULL) {
			TrieNode *newNode = new TrieNode();
			newNode->isStr = false;
			memset(newNode->next, NULL, sizeof(newNode->next));

			location->next[*word-'a'] = newNode;
		}
		location = location->next[*word-'a'];
		word++;
	}
	location->isStr = true;
}

bool Search(TrieNode *root, const char *word) {
	TrieNode *location = root;
	while (*word && location != NULL) {
		location = location->next[*word-'a'];
		word++;
	}
	return (location != NULL && location->isStr);
}

void Delete(TrieNode * location) {
	for (int i=0; i < branchNum; i++) {
		if (location->next[i] != NULL) {
			Delete(location->next[i]);
		}
	}
	delete location;
}
```
#### 总结：
勤思考。  

## 结语
不管怎么样好好加油。
