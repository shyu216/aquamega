---
date: "2024-05-02T11:13:45+10:00"
draft: false
title: "Treap"
categories:
    - COMP90077
tags: ["DS"]
params:
  math: true
---


- Tree + Heap = Treap
- Insertion: O(log n) expected, O(n) worst case
- Search: O(log n) expected, O(n) worst case
- Deletion: O(log n) expected, O(n) worst case


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