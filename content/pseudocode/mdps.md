---
date: "2024-05-02T11:13:45+10:00"
draft: false
title: "MDPs"
tags: ["comp90054"]
params:
  math: true
---



# Markov Decision Processes（MDPs）马尔可夫决策过程

MDP是完全可观察的，概率状态模型：
```
状态空间 $S$
初始状态 $s_0 \in S$
一组目标状态 $G \subseteq S$
在每个状态 $s \in S$ 中可应用的动作 $A(s) \subseteq A$
对于 $s \in S$ 和 $a \in A(s)$，有转移概率 $P_a(s'|s)$
动作成本 $c(a,s) > 0$
```

其中：
解决方案是将状态映射到动作的函数（策略）
最优解最小化预期的前往目标的成本

# Partially Observable MDPs (POMDPs) 部分可观察的马尔可夫决策过程
POMDP是部分可观察的，概率状态模型：
```
状态 $s \in S$
在每个状态 $s \in S$ 中可应用的动作 $A(s) \subseteq A$
对于 $s \in S$ 和 $a \in A(s)$，有转移概率 $P_a(s'|s)$
初始信念状态 $b_0$
最终信念状态 $b_f$
由概率 $P_a(o|s)$，$o \in Obs$ 给出的传感器模型
```

其中：
信念状态是关于 $S$ 的概率分布
解决方案是将信念状态映射到动作的策略
最优策略最小化从 $b_0$ 到 $G$ 的预期成本




*see also*: [https://gibberblot.github.io/rl-notes/single-agent/MDPs.html](https://gibberblot.github.io/rl-notes/single-agent/MDPs.html)


# Value Iteration

A kind of dynamic programming algorithm for finding the optimal policy for a Markov Decision Process (MDP).

```python
def value_iteration(states, actions, P, r, gamma, theta):
    V = {s: 0 for s in states}  # Initialize value function
    while True:
        delta = 0
        for s in states:
            v = V[s]
            V[s] = max(sum(P[s][a][s_prime] * (r[s][a][s_prime] + gamma * V[s_prime])
                            for s_prime in states) for a in actions[s])
            delta = max(delta, abs(v - V[s]))
        if delta < theta:  # Check for convergence
            break
    return V
```