---
date: "2024-05-02T11:13:45+10:00"
draft: false
title: "A*"
tags: ["comp90054"]
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