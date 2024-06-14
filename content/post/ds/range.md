---
date: 2024-06-13
draft: false
title: Range Search
categories:
    - COMP90077
tags: 
    - Data Structure
---

- 用于范围查询（一次多个值）

对于二维数据：

- 构建时间：O(n log n)
- 空间消耗：O(n log n)，log n层，每层至多n个
- 查询时间：O(k + log n)，其中 k 是报告的点的数量。


## Fractional Cascading

分数级联是一种技术，用于加速范围查询。它通过在不同层次的数据结构之间共享信息来减少查询时间。

succ和pred指针，指向下一层的元素。