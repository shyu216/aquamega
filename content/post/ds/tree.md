---
date: 2024-06-11
draft: false
title: Tree
tags: 
    - Data Structure
---

## Tree

连着的没有方向的没有圈圈的图

## Rooted Tree

有一个根节点

### Parent, Child, Sibling

- Parent: 父节点
- Child: 子节点
- Sibling: 兄弟节点
- Leaf: 没有子节点的节点
### Ancestor, Descendant
- Ancestor: 祖先节点，一个path到根节点，我是我自己的祖先
- Proper Ancestor: 除了自己的祖先
- Descendant: 子孙节点
- Proper Descendant: 除了自己的子孙

### Node depth

depth是对node说的，proper ancestor的数量，根节点的depth是0

### Height

height是对整个tree说的，最大的depth+1

## Binary Tree

每个节点最多有两个子节点的rooted tree

## Binary Search Tree

- 每个node都有一个key，可以重复
- 对于每个node，左子树的key都小于这个node的key，右子树的key都大于这个node的key

## Balanced Binary Tree

一啪啦实现方法，尽量让树的高度小，比如AVL tree，Red-Black tree

- O(log n)的search, insert, delete
- O(n)的space