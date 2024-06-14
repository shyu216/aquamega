---
date: 2024-06-13
draft: false
title: Quake Heap
categories:
    - COMP90077
tags: 
    - Data Structure
---

- 数据在leaf，整个堆用priority维护，跟实际数据无关
- Insertion: O(1) expected, O(log n) worst case
- Search: N/A (or O(n) if heap is traversed)
- Decrease Key: O(1) expected, O(n) worst case
- Deletion (Delete Min): O(log n) expected, O(n) worst case

Quake Heaps 是一种优先队列数据结构，它在处理动态集合中的元素和执行相关操作（如插入、删除、查找最小元素等）时，提供了良好的时间复杂性。Quake Heaps 的一个关键特性是它们的删除操作的摊还时间复杂度为 $O(\log n)$，这使得它们在需要频繁删除操作的应用中非常有用。

以下是一些可能使用 Quake Heaps 的应用：

1. **图算法**：许多图算法，如 Dijkstra 的最短路径算法和 Prim 的最小生成树算法，需要使用优先队列来高效地找到下一个要处理的节点。在这些算法中，Quake Heaps 可以用来提高性能。

2. **事件驱动的模拟**：在事件驱动的模拟中，事件是按照它们发生的时间顺序处理的。Quake Heaps 可以用来存储和检索这些事件，以确保它们按照正确的顺序被处理。

3. **任务调度**：在任务调度问题中，我们需要根据任务的优先级来决定执行顺序。Quake Heaps 可以用来存储和检索任务，以确保优先级最高的任务首先被执行。

请注意，虽然 Quake Heaps 在理论上有很好的性能，但在实践中，由于它们的实现复杂性，可能会选择其他更简单但性能稍差的数据结构，如 Fibonacci heaps 或 binary heaps。

## Tournament Trees

Quake Heaps 是基于 Tournament Trees 的一种改进。Tournament Trees 是一种完全二叉树，其中每个节点都包含一个元素，并且树的叶子节点是输入元素。在 Tournament Trees 中，每个节点都存储了其子树中的最小元素。这使得 Tournament Trees 可以用来高效地找到最小元素。

## Pointers

P即T的最后一层，每个节点都是一个元素。

1. **元素指针**：在优先队列 P 中，每个元素都保持一个指向 Tournament Tree T 中概念上存储其优先级的最高节点（即，高度最大的节点）的指针。

2. **节点指针**：在 Tournament Tree T 中，每个节点 u 都有一个指向优先队列 P 中的元素的指针，u 概念上存储了该元素的优先级。




## Node-Number-at-Height Invariant

在 Quake Heaps 中，有一个重要的不变性，即“高度 h 处的节点数目”不变性。

有一个constant $c$，上一层的节点数目是下一层的节点数目的 $c$ 倍。这个不变性保证了 Quake Heaps 的高效性。

```
c = 0.6
n5 = 1
n4 = 3
n3 = 5
n2 = 9
n1 = 15
```

$n_{h+1} \leq c \cdot n_h$

## log n

1. 最后一层至多n个
2. 每层会少c倍
3. 层数至多$\log_{1/c} n$



## Operations

### Link 

将两个 Tournament Trees 连接成一个更大的 Tournament Tree。这个操作的时间复杂度是 $O(1)$。

条件：两个 Tournament Trees 的高度相同。

### Cut

切根和较大的子节点。这个操作的时间复杂度是 $O(1)$。

### Insert

直接插入，建个新树。这个操作的时间复杂度是 $O(1)$。

### Decrease Key

降低一个元素的优先级。把它的值减小，找到它指的树中的节点，然后cut。这个操作的时间复杂度是 $O(1)$。

### Delete Min

找到最小的元素，删掉整个path。通常先经过decrease key，使目标数据有最小priority，操作更方便。要是有same height，link起来。

这个操作的时间复杂度是 $O(\log n)$，可以用admortized analysis证明。

- 跟树的数量，和path的长度有关。


1. 找到具有最小键值的元素。
   - 有T个树，需T步
2. 删除这个元素。
   - 如path长L，有L步  
   - 1和2共T+L
3. 同一高度的树合并。while loop
   - T-1个其他树，切掉path后有L个新树，共T+L-1步
   - 仅需T+L-2个合并，因为至少剩下一个树
   - $T^{(1)} \leq 2h^{(0)}_{max}$，合并后的树的数量小于等于合并前最高的树的高度的2倍
4. 保持不变性。
   - 只会删node，而不加，把不符的高层整层删掉，$\Delta N < 0$
   - 新增的树不会比新的最高层的node多，$\Delta T \leq n^{(0)}_h$
   - 只会删坏节点，而不加，按层删的，所以就算往上一层h+1坏节点。这一层的节点数是两倍上一层的好节点和一倍上一层的坏节点，所以$n_h = 2(n_{h+1} - b_{h+1}) + 1*b_{h+1}$


## Admortized Analysis

N个元素，T个树，B个坏节点（只有一个孩子）

$\Phi = N + 3T + \frac{3}{2\alpha -1}B$

## $T^{(1)} \leq 2h^{(0)}_{max}$

- 每种高度的树最多有一个，不然就被合并了
- 合并后的高度至多是原来的两倍
- 合并前至多有$h^{(0)}_{max}$种高度的树，每种合并一次，最后高度会是$2h^{(0)}_{max}$