---
date: 2024-05-02
draft: false
title: "Treap"
categories:
    - COMP90077
tags: 
    - Data Structure
---


- Tree + Heap = Treap
- Insertion: O(log n) expected, O(n) worst case
- Search: O(log n) expected, O(n) worst case
- Deletion: O(log n) expected, O(n) worst case

treap的key是有用的数据；priority是随机生成的值，用于保持treap的平衡。

## Operations

### Insertion

加到叶子节点，然后向上旋转，直到满足treap的性质。

### Deletion

找到要删除的节点，把priority设为无穷大，然后旋转，直到满足treap的性质。此时，要删除的节点就变成了叶子节点，然后删除。

### Search

和BST一样，递归地搜索左子树或右子树。

### Join

搞一个假的节点，priority设为无穷大，然后把两个treap的根节点作为左右子树，然后旋转，直到满足treap的性质。

### Split

把要split的key找到，设成无穷小，然后旋转，直到满足treap的性质。此时，这个key到根节点了。


## Implementation

```python
import random

class Node:
    def __init__(self, id, key, priority):
        self.id = id
        self.key = key
        self.priority = priority
        self.left = None
        self.right = None

class Treap:
    def __init__(self):
        self.root = None

    def _left_rotate(self, node):
        right_child = node.right
        node.right = right_child.left
        right_child.left = node
        return right_child

    def _right_rotate(self, node):
        left_child = node.left
        node.left = left_child.right
        left_child.right = node
        return left_child

    def insert(self, element):
        node = Node(element[0], element[1], random.random())
        if not self.root:
            self.root = node
            return
        self.root = self._insert_node(self.root, node)

    def _insert_node(self, root, node):
        if not root:
            return node
        if node.key < root.key:
            root.left = self._insert_node(root.left, node)
            if root.left.priority > root.priority:
                root = self._right_rotate(root)
        else:
            root.right = self._insert_node(root.right, node)
            if root.right.priority > root.priority:
                root = self._left_rotate(root)
        return root

    def delete(self, keydel):
        self.root = self._delete_node(self.root, keydel)

    def _delete_node(self, root, keydel):
        if not root:
            return None
        if keydel < root.key:
            root.left = self._delete_node(root.left, keydel)
        elif keydel > root.key:
            root.right = self._delete_node(root.right, keydel)
        else:
            if not root.left and not root.right:
                root = None
            elif not root.left:
                root = root.right
            elif not root.right:
                root = root.left
            else:
                if root.left.priority < root.right.priority:
                    root = self._right_rotate(root)
                    root.right = self._delete_node(root.right, keydel)
                else:
                    root = self._left_rotate(root)
                    root.left = self._delete_node(root.left, keydel)
        return root

    def search(self, key):
        return self._search_node(self.root, key)

    def _search_node(self, root, key):
        if not root:
            return None
        if root.key == key:
            return (root.id, root.key)
        elif key < root.key:
            return self._search_node(root.left, key)
        else:
            return self._search_node(root.right, key)