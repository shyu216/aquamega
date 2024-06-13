---
date: 2024-05-02
draft: false
title: "Dynamic Array"
categories:
    - COMP90077
tags: 
    - Data Structure
---

- Insertion: O(1) expected, O(n) worst case
- Search: O(n) expected, O(n) worst case
- Deletion: O(n) expected, O(n) worst case


```python
class DynamicArray:
    def __init__(self):
        self.n = 0  # Number of elements
        self.capacity = 1  # Initial capacity
        self.A = self._make_array(self.capacity)

    def __len__(self):
        return self.n

    def __getitem__(self, k):
        if not 0 <= k < self.n:
            raise IndexError('invalid index')
        return self.A[k]

    def insert(self, element):
        """
        element = (id,key)
        """
        if self.n == self.capacity:
            self._resize(2 * self.capacity)
        self.A[self.n] = element
        self.n += 1

    def delete(self, keydel):
        for i in range(self.n):
            if self.A[i][1] == keydel:
                self.A[i], self.A[self.n - 1] = self.A[self.n - 1], self.A[i]
                self.n -= 1
                if self.n > 0 and self.n <= self.capacity // 4:
                    self._resize(self.capacity // 2)
                break

    def search(self, keysch):
        for element in self.A[:self.n]:
            if element[1] == keysch:
                return element
        return None

    def _resize(self, new_cap):
        B = self._make_array(new_cap)
        for k in range(self.n):
            B[k] = self.A[k]
        self.A = B
        self.capacity = new_cap

    def _make_array(self, new_cap):
        return [None] * new_cap
```