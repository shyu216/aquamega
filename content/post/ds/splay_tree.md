---
date: 2024-06-13
draft: false
title: Splay Tree
categories:
    - COMP90077
tags: 
    - Data Structure
---

- 越常访问，越靠近root
- 一种balanced BST，但不保证平衡
- Insertion: O(log n) expected, O(n) worst case
- Search: O(log n) expected, O(n) worst case
- Deletion: O(log n) expected, O(n) worst case

## Zig-Zig and Zag-Zag

left-left/right-right turns to right-right/left-left

## Zig-Zag and Zag-Zig

turns to middle

## Zig and Zag

just swap

## Successful-search-only sequence

"Successful-search-only sequence" 是一种特定的操作序列，其中只包含成功的搜索操作。在这种序列中，所有的搜索操作都能找到它们正在寻找的元素。

这种操作序列在分析某些数据结构的性能时非常有用。例如，当我们分析哈希表的性能时，我们可能会考虑最坏情况下的操作序列，其中包含大量的失败的搜索操作。然而，在实际应用中，失败的搜索操作可能非常少，因此，考虑 "successful-search-only sequence" 可能会给出更准确的性能分析。

在 "successful-search-only sequence" 中，由于所有的搜索操作都是成功的，所以数据结构的性能主要取决于如何高效地存储和检索元素。因此，这种操作序列对于理解和优化数据结构的性能非常有用。

## Information theory

信息理论能够帮助我们理解数据结构的性能。在信息理论中，我们可以使用熵来衡量数据的不确定性。熵越高，数据的不确定性就越大。

它可以用来界定最优的成本界限。