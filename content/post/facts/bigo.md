---
date: 2024-06-11
draft: false
title: log n，n，2^n的关系
tags: 
    - Facts
    - Analysis
categories:
    - COMP90077
---

##  Big-O Notation

$$ f(n) \in O(g(n)) \text{ iff } \exists c_1, c_2, \forall  n > c_2,  f(n) \leq c_1 \cdot g(n)$$


## $O(\log n) \subset O(n^k) \subset O(2^n)$

求证？设新方程，用相除或相减把不等式移到同一边，然后证明单调性，且大于1或大于0，取得$c_1, c_2$的值。