---
date: "2024-05-29T11:13:45+10:00"
draft: false
title: "UCB and Greedy BFS"
categories:
    - COMP90054
tags: ["algo"]
params:
  math: true
---

# Uniform Cost Search

Priority Queue，最先被探索离起始节点最近（即路径成本最低）的节点。


Breath First Search属于Uniform Cost Search的特例，即每个节点的路径成本都是1。


UCS只看到了路径成本，没有考虑启发式。

```python
def uniformCostSearch(problem):
    candidate_pq = util.PriorityQueue()
    init_state = problem.getStartState()
    init_path = []
    candidate_pq.push((init_state,init_path),0)
    viewed = []
    while not candidate_pq.isEmpty():
        state,path = candidate_pq.pop()
        if problem.isGoalState(state):
            return path
        if state not in viewed:
            viewed.append(state)
            for child_state, child_action, child_cost in problem.getSuccessors(state):
                child_path = path + [child_action]
                candidate_pq.push((child_state,child_path),problem.getCostOfActions(child_path))
    return None
```

# Greedy Best First Search

BFS只看到了启发式，没有考虑路径成本。

If h=0，BFS是什么根据它的Priority Queue的实现。

```python
def bestFirstSearch(problem, heuristic=nullHeuristic):
    candidate_pq = util.PriorityQueue()
    init_state = problem.getStartState()
    init_path = []
    candidate_pq.push((init_state,init_path),heuristic(init_state, problem))
    viewed = []
    while not candidate_pq.isEmpty():
        state,path = candidate_pq.pop()
        if problem.isGoalState(state):
            return path
        if state not in viewed:
            viewed.append(state)
            for child_state, child_action, _ in problem.getSuccessors(state): # ignore cost as we are blind
                child_path = path + [child_action]
                candidate_pq.push((child_state,child_path),heuristic(child_state, problem))
    return None
```