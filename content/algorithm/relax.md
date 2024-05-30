---
date: "2024-05-29T11:13:45+10:00"
draft: false
title: "Greedy Relaxed Planning"
tags: ["comp90054"]
params:
  math: true
---



- h*: the optimal heuristic
- h pre&del: the heuristic ignoring preconditions and delete effects, adimissible and consistent, "subset sum" problem, NP-hard
- h goal_count: the number of goals not yet achieved, neither admissible nor consistent
- h+/h del: admitssible and consistent, 相当于MST, 每个state只访问一遍，也NP-hard
- h add: easily not admissible
- h max: easily too small
- h ff: use h add and h max


- Removing preconditions and delete effects is efficiently constructive but not computable。

- h max和h add的table是不一样的，一个是最大值，一个是累加值。




# Delete Relaxation

忽略搜索中所有的delete效果，在发现goal之前减少重复的状态。

- State Dominance: 如果一个状态支配另一个状态，那么我们可以忽略支配状态。被包含了。


```python
def greedyRelaxedPlan(problem):
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
            for child_state, child_action, _ in problem.getSuccessors(state): # ignore cost as we are blind
                child_path = path + [child_action]
                candidate_pq.push((child_state,child_path),0)
    return None
```

Neither admissible nor consistent. 因为不保证optimal，只保证能找到解决方案。

Optimal的都NP-hard。


# Additive and Max Heuristics

- Additive: 相加子目标的启发式，明显不是admissible。
- Max: 选择子目标中最大的启发式。最难解决的子节点。

都goal-aware，因为h+ ∞时，h也是∞。

# Best Supporter Heuristic

- 把$h_{add}$和$h_{max}$结合起来，选择最好的支持者。

- argmin: 在一系列动作里，选最小的h。

# Bellman-Ford for hmax and hadd

Bellman-Ford variant computing hadd for state s

反复更新表Tadd，直到表中的值不再改变。在每次迭代中，对于每个目标状态g，都会计算一个新的值fi(g)，这个值是当前状态s到状态g的最短路径的估计值。

```python
def bellmanFordHadd(problem):
    states = problem.getStates()
    actions = problem.getActions()
    P = problem.getTransitionProbabilities()
    r = problem.getRewards()
    gamma = problem.getDiscount()
    theta = 0.01
    Tadd = {s: 0 for s in states}
    while True:
        delta = 0
        for s in states:
            v = Tadd[s]
            Tadd[s] = min([sum([r[s][a][s_prime] + gamma * Tadd[s_prime] for s_prime in states]) for a in actions])
            delta = max(delta, abs(v - Tadd[s]))
        if delta < theta:
            break
    return Tadd
```



# Iterated Width

Novelty：只考虑$w(s)$个状态变量atoms的变化情况。

搜索直到目标状态的状态变量的数量。

一个state的novelty：第一次出现的atom组合中的atom数量。the size of the smallest subset of atoms in s，that is true for the first time in search。