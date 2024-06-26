---
date: 2024-06-11
draft: false
title: Max-Flow Min-Cut Theorem
categories:
    - COMP90077
tags: 
    - algorithm
---

**请注意**！本文是由公元2024年的GPT生成的，可能包含一些不准确的信息。

最大流（Max-Flow）问题和最小割（Min-Cut）问题在网络流中是两个互相关联的问题，它们的关系通常被称为最大流-最小割定理（Max-Flow Min-Cut Theorem）。

最大流-最小割定理是网络流中的一个基本定理，它指出了一个网络的最大流量和该网络的最小割的容量之间的关系。具体来说，对于任何网络，其最大流量等于其最小割的容量。

在一个网络流图中，流量从源节点（source）流向汇节点（sink）。最大流问题就是要找到一种流的分配方式，使得从源节点到汇节点的总流量最大。

割（cut）是将网络图分割成两部分的一种方式，其中一部分包含源节点，另一部分包含汇节点。割的容量（capacity）是从源节点部分到汇节点部分的所有边的容量之和。最小割问题就是要找到一种割的方式，使得割的容量最小。

## Karger's Algorithm for Min Cut

David Karger 的最小割算法是一种随机化算法，用于在无向图中找到最小割。这个算法基于一种称为“边收缩”（edge contraction）的操作。

这个算法的期望运行时间是多项式的，但是它可能需要多次运行才能找到真正的最小割。为了提高找到最小割的概率，我们可以多次运行这个算法，并返回所有运行中找到的最小割。

1. Adjacency list
   
    邻接列表是一种表示图的方法，它为图中的每个顶点维护一个列表，列出了从该顶点出发可以到达的所有顶点。在 Python 中，我们通常使用字典来实现邻接列表，其中键是顶点，值是一个列表，包含了所有连接到该顶点的顶点。邻接列表是一种空间效率高的数据结构，特别适合于稀疏图，即边的数量远小于顶点的数量的平方的图。


2. Union-Find

    并查集是一种用于处理不相交集合的数据结构。它支持两种操作：查找和合并。查找操作 Find(x) 用于找到包含元素 x 的集合的代表元素。合并操作 Merge(x, y) 用于将包含元素 x 和 y 的两个集合合并为一个集合。并查集的一个重要特性是，这两种操作的时间复杂度都接近于常数，这使得它在处理大规模数据时非常高效。

## Greedy Algorithm for Max Flow 

1. 初始化所有边的流量为0。
2. 寻找一条从源点s到目标点t的路径，这条路径上的每一条边的流量都小于其容量。
3. 沿着找到的这条路径尽可能多地增加流量，找到路径上剩余容量最小的边，然后增加这个量的流量。

我们重复以上步骤，直到无法找到满足条件的路径为止。

- 无法保证最优。贪心算法可能会选择一条在当前看来可以增加最多流量的路径。然而，这可能会导致在后续的步骤中，无法找到新的路径来进一步增加流量。

## Ford-Fulkerson Algorithm for Max Flow 

Ford-Fulkerson 算法是一种解决最大流问题的经典方法。这个算法的基本步骤如下：

1. 初始流设为零。
2. 只要在残余网络中存在一条从源节点 s 到汇点 t 的路径，就执行以下操作：
   - 寻找一条可以增加流量的路径。
   - 更新流量和残余网络。
3. 返回最后计算出的流量。

### Proofs

- 在每一次迭代中，流量都是整数：这可以通过数学归纳法来证明。初始的流量是零，是一个整数。在每次迭代中，我们都在一条路径上增加整数的流量，所以流量始终是整数。

- 在每次迭代中，流量增加了 KP：这可以通过观察源节点 s 和路径来证明。在每次迭代中，我们都在一条从 s 到 t 的路径上增加流量，所以总流量会增加。

- 算法会在有限的步骤后停止（最多在 𝐶 = ∑(对所有边的容量𝑐求和) 迭代后）：这可以从前面的证明推断出来。因为每次迭代都会增加流量，而总流量受到网络容量的限制，所以算法一定会在有限的步骤后停止。

### Running time

Ford-Fulkerson（FF）算法的运行时间取决于多个因素，包括图的结构、边的容量以及选择增广路径的策略。在每次迭代中，算法需要在残余图中找到一条源节点s到目标节点t的路径，然后根据这条路径更新流量和残余图。

每次迭代的时间复杂度为O(m)，其中m是图中的边的数量，原因如下：

1. 在残余图中找到一条s-t路径：这可以通过深度优先搜索（DFS）或广度优先搜索（BFS）来完成，时间复杂度为O(m)。

2. 更新流量和残余图：一旦找到了一条增广路径，我们需要遍历这条路径上的所有边，更新它们的流量和残余容量。这个过程的时间复杂度也为O(m)，因为一条路径上的边的数量最多为m。

因此，每次迭代的时间复杂度为O(m)。然而，需要注意的是，FF算法的总运行时间并不是多项式时间，因为算法的迭代次数取决于最大流量，而这可能远大于图的大小。

循环的次数最多是 C，其中 C 是图中所有边的容量之和。这是因为在每次循环中，我们至少增加一单位的流量，因此最多需要 C 次循环。

因此，总的运行时间是 O(Cm)。而实际情况一般是线性时间。

#### Flow vs Cut

在最大流最小割定理中，流等于割是因为在流网络中，流的大小受限于割的容量。这个定理告诉我们，任何流网络的最大流都等于其某个割的最小容量。

这是因为：

1. 流的大小不能超过任何割的容量。这是因为割定义了从源点到汇点的所有可能的路径，流必须通过这些路径，因此不能超过割的容量。

2. 在最大流的情况下，存在一个割，其容量等于流的大小。这是因为当我们找到最大流时，我们已经找到了一种方式，使得所有从源点到汇点的路径都被充分利用，这就形成了一个割。

在最大流最小割定理中，可达性（reachability）的概念是非常重要的。我们可以通过以下步骤使用可达性来证明这个定理：

1. 首先，我们找到流网络中的一个最大流。在这个流中，我们可以找到一个割，即一个将网络分割成两部分的边集，使得所有的流都从割的一边（源点所在的一边）流向另一边（汇点所在的一边）。

2. 然后，我们考虑在残余网络中从源点开始的可达性。在残余网络中，一个节点是可达的，如果存在一条从源点到该节点的路径，路径上的所有边在残余网络中都有正的容量。

3. 在最大流的情况下，汇点在残余网络中是不可达的，因为所有的流都已经达到了最大值，没有更多的容量可以从源点流向汇点。这意味着存在一个割，将可达的节点和不可达的节点分开，割的容量等于最大流的值。

4. 因此，我们证明了最大流等于最小割。这是因为我们找到了一个割，其容量等于最大流的值，而任何其他割的容量必须大于或等于这个值，因为流的大小不能超过割的容量。所以，这个割就是最小割，其容量（即最小割的值）等于最大流的值。

#### Flow-Value Lemma

流量值引理（Flow-Value Lemma）是网络流问题中的一个重要概念，它描述了流入和流出一个节点的总流量之间的关系。

流量值引理的内容如下：

对于任何流网络中的节点 v（除了源点 s 和汇点 t），流入节点 v 的总流量等于流出节点 v 的总流量。这个性质也被称为流的守恒性质，因为它意味着除了源点和汇点之外，没有流量在任何节点处被创建或消失。

数学上，这可以表示为：

对于所有节点 v（v ≠ s, v ≠ t），∑_{u ∈ V} f(u, v) = ∑_{u ∈ V} f(v, u)

其中 V 是节点的集合，f(u, v) 是从节点 u 到节点 v 的流量。

这个引理是网络流问题中的基本性质，它是许多网络流算法，包括 Ford-Fulkerson 算法和 Edmonds-Karp 算法的基础。

#### Weak Duality

弱对偶性（Weak Duality）在流量值特征（flow value characterization）中的应用是网络流问题的一个重要概念。它提供了流量值的一个上界。

弱对偶性定理的内容如下：

对于任何流网络和任何割（s-t cut），流量值总是小于或等于割的容量。换句话说，最大流的值总是小于或等于最小割的值。

在流量值特征中，这个定理意味着我们可以通过寻找最小割来得到流量值的一个上界。这个上界对于理解和解决网络流问题非常有用，因为它提供了一个我们无法超过的流量值。

此外，这个定理还证明了最大流最小割定理（Max-Flow Min-Cut Theorem）的一部分。最大流最小割定理是网络流问题中的一个重要定理，它表明在任何流网络中，最大流的值等于最小割的值。弱对偶性定理证明了这个定理的“小于等于”部分，而“等于”部分需要通过 Ford-Fulkerson 算法或其变种来证明。

### Optimality

所有穿过割的边要么是从 A 到 B 并且满流，要么是从 B 到 A 并且空流。

## Perfect Matchings

在图论中，"匹配"（Matching）是指图的一个边的子集，使得子集中的任意两条边都不共享顶点。这是一种将图中的一部分顶点配对的方式，每对配对都通过一条边连接。匹配不一定需要包含图中的所有顶点。

"完美匹配"（Perfect Matching）是匹配的一种特殊情况。在完美匹配中，图的每个顶点都恰好与子集中的一条边相连。换句话说，如果一个图有 n 个顶点，那么它的一个完美匹配就会有 n/2 条边。

完美匹配在许多问题中都有应用，例如在网络设计、任务分配、市场匹配等问题中。在这些问题中，我们通常希望找到一个完美匹配，使得某种成本或效益最优化。

例如，二分图的最大匹配问题就是要找到一个最大的匹配，即一个最大的边集，使得集合中的任意两条边都不共享端点。这个问题可以通过将其转化为最大流问题来解决。

## Bipartite Matching

二分匹配（Bipartite Matching）是图论中的一个重要概念，它是在二分图（Bipartite Graph）中进行的匹配。

二分图是一种特殊的图，它的所有顶点可以被分成两个互不相交的集合，使得每一条边的两个端点分别属于这两个不同的集合。在二分图中进行匹配，就是找到边的集合，使得在这个集合中的任意两条边都不共享端点。

二分匹配有许多实际应用，例如在任务分配、稳定婚姻问题、市场均衡等问题中都有应用。在这些问题中，我们通常希望找到一个最大的匹配，也就是包含最多边的匹配。

加s和t就能当max-flow问题解了。

"请说'相邻'而不是'连接'"：在图论中，"相邻"和"连接"这两个词有着不同的含义。如果两个节点之间有一条边，我们通常说这两个节点是"相邻"的。而"连接"通常指的是在一个图中，存在一条路径可以从一个节点到达另一个节点。

"避免使用'任何'这个词"：在描述算法时，"任何"这个词可能会引起混淆。比如，如果我们说"任何节点都可以到达任何其他节点"，这可能会被误解为在图中存在一条从每个节点到每个其他节点的直接边，而实际上我们可能只是想表达在图中存在一条从每个节点到每个其他节点的路径。

### Integrality Theorem

整数定理（Integrality Theorem）是网络流问题中的一个重要定理，它表明如果所有边的容量都是整数，那么存在一个最大流，使得每条边的流量也都是整数。

如果 k 是整数，并且我们只考虑容量为 1 的边，那么每条边的流量 f(e) 必须是 0 或 1。原因是流量必须满足容量约束，也就是说，流量不能超过容量。因此，如果容量为 1，那么流量只能是 0 或 1。

这个性质在解决一些特殊的网络流问题时非常有用，例如在匹配问题和路由问题中。在这些问题中，我们通常只关心是否存在一条边，而不关心边的具体容量，所以我们可以将所有边的容量设为 1，然后应用整数定理。

### Match to Flow

这个定理表明，在图 G 中的最大匹配数等于在 G' 中的最大流量。这个定理的证明分为两部分：

1. ≤：将最大匹配转化为流量。匹配约束确保我们满足流量约束。匹配约束和匹配大小确保流量值等于匹配大小。

2. ≥：将最大流量转化为匹配。流量整数性确保我们不会选择边的分数部分。流网络的约束（容量，保守性）确保我们满足匹配约束（每个顶点最多只能与一个匹配边相邻）。流量值引理表明匹配的大小等于流量的值。

这个定理说明了匹配问题和网络流问题之间的深刻联系。通过将匹配问题转化为网络流问题，我们可以使用网络流算法，如 Ford-Fulkerson 算法和 Edmonds-Karp 算法，来解决匹配问题。这种转化方法在解决一些复杂的组合优化问题时非常有用。

## Disjoint Paths

在图论中，"不相交路径"（Disjoint Paths）是指一组路径，其中任意两条路径都没有共享的顶点或边。换句话说，这些路径是完全独立的，它们不会在任何地方交叉或重叠。

不相交路径的概念在许多问题中都有应用，例如在网络设计、路由问题、交通规划等问题中。在这些问题中，我们通常希望找到一组不相交的路径，以便最大化网络的吞吐量，或者避免交通拥堵。

在有向图中，我们可以通过最大流算法来找出k条边不相交的路径。这个问题可以转化为一个容量为1的最大流问题。

以下是证明过程：

1. **只需证明**：假设我们有k条不相交的路径。我们可以在每条路径上路由一单位的流，不需要其他流。因此，最大流至少为k。

2. **如果证明**：假设最大流至少为k。我们需要证明存在至少k条不相交的路径。为了证明这一点，我们可以对携带流的边的数量进行归纳。

   归纳基础：如果最大流为1，那么存在一条从s到t的路径。

   归纳步骤：假设对于所有小于k的最大流，都存在相应数量的不相交路径。现在，我们考虑最大流为k的情况。由于流的整数性质，我们知道存在一条边，其流量为1，我们可以移除这条边，并将总流量减少1。根据归纳假设，剩余的图存在k-1条不相交的路径。加上我们刚才移除的那条边，我们就找到了k条不相交的路径。

因此，我们可以得出结论：在有向图中，存在k条边不相交的路径当且仅当最大流至少为k。

## Scaling Max Flow

在解决最大流问题时，一种常用的策略是使用缩放（Scaling）技术。这种技术的基本思想是先解决一个简化的问题，然后逐步增加问题的规模，直到解决原始问题。

在最大流问题中，缩放技术通常是这样实现的：

1. 首先，我们找到网络中最大的容量 C。

2. 然后，我们设置一个阈值，初始值为 C。

3. 我们只考虑容量大于或等于阈值的边，忽略其他边，然后使用 Ford-Fulkerson 算法或 Edmonds-Karp 算法找到这个简化网络的最大流。

4. 然后，我们将阈值减半，再次运行最大流算法。

5. 我们重复这个过程，直到阈值为 1。

这种方法的优点是，每次迭代时，我们只需要考虑一部分边，这可以大大减少计算量。此外，由于我们是从大到小逐步减小阈值，所以我们可以利用前一次迭代的结果，这可以进一步提高效率。

这种方法在处理大规模网络流问题时非常有效，特别是当网络中的容量差异很大时。

## Edmonds-Karp Algorithm

1. 找最宽的路径。Dijkstra,$O(m^2lognlogF)$
2. 找最短的路径。BFS,$O(m^2n)$

## Applications

### Circulation with Demands

多个源点和汇点的网络流问题是网络流问题的一个重要变种。在这个问题中，我们有多个源点和多个汇点，每个源点都有一个流出的需求，每个汇点都有一个流入的需求。我们的目标是找到一种流的分配方式，使得每个源点的流出等于需求，每个汇点的流入等于需求。



## Hall’s Theorem


哈尔定理（Hall's Theorem）是图论中的一个重要定理，主要用于解决二部图的完美匹配问题。它的内容如下：

在一个二部图中，如果对于左侧的每个顶点集合，其邻接的右侧顶点集合的大小至少与其一样大，那么这个二部图存在一个完美匹配。

更形式化地说，设 G=(V,E) 是一个二部图，V 可以分为两个部分 V1 和 V2。如果对于 V1 中的任意子集 S，都有 |N(S)| >= |S|，其中 N(S) 是 S 中所有顶点的邻接顶点集合，那么 G 中存在一个完美匹配。

这个定理在组合优化、网络流和匹配理论等领域有广泛的应用。例如，它可以用来解决任务分配问题、婚配问题等。


Hall定理是用于解决二部图中的完美匹配问题的，而流网络中的需求循环问题则需要使用不同的方法来解决。

在流网络中，每个节点都有一个需求，表示流入该节点的流量和流出该节点的流量之间的差值。一个需求循环是一个满足所有节点需求的流。

要解决需求循环问题，我们可以使用以下步骤：

1. 添加一个新的源节点s和一个新的汇点t。
2. 对于每个需求为d的节点v，如果d > 0，那么添加一条从s到v的边，容量为d；如果d < 0，那么添加一条从v到t的边，容量为-d。
3. 在新的网络中找到一个最大流。如果这个最大流的值等于所有正需求的总和，那么原网络存在一个需求循环。否则，原网络不存在需求循环。

这个方法的正确性基于最大流最小割定理：在一个流网络中，最大流的值等于最小割的容量。在这个问题中，最小割就是将所有正需求的节点和所有负需求的节点分开的割，其容量就是所有正需求的总和。所以，如果最大流的值等于所有正需求的总和，那么就存在一个需求循环。反之，如果存在一个需求循环，那么最大流的值必然等于所有正需求的总和。