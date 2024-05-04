---
date: "2024-05-02T11:13:45+10:00"
draft: false
title: "BFS"
tags: ["comp90054"]
params:
  math: true
---

# 广度优先搜索（BFS）

队列，先进先出，后进后出。

```python
def breadthFirstSearch(problem):
    candidate_queue = util.Queue()
    init_state = problem.getStartState()
    init_path = []
    candidate_queue.push((init_state,init_path))
    viewed = []
    while not candidate_queue.isEmpty():
        state,path = candidate_queue.pop()
        if problem.isGoalState(state):
            return path
        if state not in viewed:
            viewed.append(state)
            for child_state, child_action, _ in problem.getSuccessors(state): # ignore cost as we are blind
                child_path = path + [child_action]
                candidate_queue.push((child_state,child_path))
    return None
```