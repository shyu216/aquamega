---
date: "2024-05-02T11:13:45+10:00"
draft: false
title: "A* and Hill Climbing"
categories:
    - COMP90054
tags: ["algo"]
params:
  math: true
---


# A*算法（带有重复检测和重新打开）

```
设 open 为新的优先级队列，按照 g(state(σ)) + h(state(σ)) 升序排列
open.insert(make-root-node(init()))
设 closed 为空集
设 best-g 为空集 /* 将状态映射到数字 */
当 open 不为空时：
    σ := open.pop-min()
    如果 state(σ) 不在 closed 中或 g(σ) < best-g(state(σ))：
        /* 如果 g 更好则重新打开；注意所有具有相同状态但 g 较差的 σ′ 都在 open 中位于 σ 后面，并且在轮到它们时将被跳过 */
        closed := closed ∪{state(σ)}
        best-g(state(σ)) := g(σ)
        如果 is-goal(state(σ))：返回 extract-solution(σ)
        对于每个 (a,s′) ∈succ(state(σ))：
            σ′ := make-node(σ,a,s′)
            如果 h(state(σ′)) < ∞：open.insert(σ′)
返回 unsolvable
```

```python
def aStarSearch(problem, heuristic=nullHeuristic):
    """Search the node that has the lowest combined cost and heuristic first."""
    myPQ = util.PriorityQueue()
    startState = problem.getStartState()
    startNode = (startState, 0, [])
    myPQ.push(startNode, heuristic(startState, problem))
    best_g = dict()
    while not myPQ.isEmpty():
        node = myPQ.pop()
        state, cost, path = node
        if (not state in best_g) or (cost < best_g[state]):
            best_g[state] = cost
            if problem.isGoalState(state):
                return path
            for succ in problem.getSuccessors(state):
                succState, succAction, succCost = succ
                new_cost = cost + succCost
                newNode = (succState, new_cost, path + [succAction])
                myPQ.push(newNode, heuristic(succState, problem) + new_cost)

    return None  # Goal not found
```

If h=0, A* is equivalent to Uniform Cost Search.

If h admissible, A* is optimal. 因为我们的h比最优h小，在达到最优h之前，我们已经尝试过这个状态。

# Weighted A*算法

给heuristic函数加权，以调整搜索的速度。

w越大，搜索越快，但可能会错过最优解，w越小，搜索越慢，但更有可能找到最优解。

w=0时，等价于Uniform Cost Search。

w to ∞时，等价于Greedy Best First Search。

```python
def weightedAStarSearch(problem, heuristic=nullHeuristic, weight=1):
    """Search the node that has the lowest combined cost and heuristic first."""
    myPQ = util.PriorityQueue()
    startState = problem.getStartState()
    startNode = (startState, 0, [])
    myPQ.push(startNode, weight * heuristic(startState, problem))
    best_g = dict()
    while not myPQ.isEmpty():
        node = myPQ.pop()
        state, cost, path = node
        if (not state in best_g) or (cost < best_g[state]):
            best_g[state] = cost
            if problem.isGoalState(state):
                return path
            for succ in problem.getSuccessors(state):
                succState, succAction, succCost = succ
                new_cost = cost + succCost
                newNode = (succState, new_cost, path + [succAction])
                myPQ.push(newNode, weight * heuristic(succState, problem) + new_cost)

    return None  # Goal not found
```



# 爬山算法

local最优。

```
σ := make-root-node(init())
永远执行以下操作：
    如果 is-goal(state(σ))：
        返回 extract-solution(σ)
    Σ′ := {make-node(σ,a,s′) |(a,s′) ∈succ(state(σ)) }
    σ := 选择 Σ′ 中 h 值最小的元素 /* （随机打破平局） */
```