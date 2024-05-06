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

状态空间 $S$ \
初始状态 $s_0 \in S$ \
一组目标状态 $G \subseteq S$ \
在每个状态 $s \in S$ 中可应用的动作 $A(s) \subseteq A$ \
对于 $s \in S$ 和 $a \in A(s)$，有转移概率 $P_a(s'|s)$ \
动作成本 $c(a,s) > 0$


其中：\
解决方案是将状态映射到动作的函数（策略）\
最优解最小化预期的前往目标的成本

# Partially Observable MDPs (POMDPs) 部分可观察的马尔可夫决策过程
POMDP是部分可观察的，概率状态模型：

状态 $s \in S$ \
在每个状态 $s \in S$ 中可应用的动作 $A(s) \subseteq A$ \
对于 $s \in S$ 和 $a \in A(s)$，有转移概率 $P_a(s'|s)$ \
初始信念状态 $b_0$ \
最终信念状态 $b_f$ \
由概率 $P_a(o|s)$，$o \in Obs$ 给出的传感器模型


其中：\
信念状态是关于 $S$ 的概率分布 \
解决方案是将信念状态映射到动作的策略 \
最优策略最小化从 $b_0$ 到 $G$ 的预期成本




*see also*: [https://gibberblot.github.io/rl-notes/single-agent/MDPs.html](https://gibberblot.github.io/rl-notes/single-agent/MDPs.html)


# Value Iteration

一种动态规划算法，用于计算MDP的最优策略。

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

## Bellman Optimality Equation

利用了Bellman最优方程：
$$
V^*(s) = \max_{a \in A(s)} \sum_{s'} P_a(s'|s) \left[ R_a(s'|s) + \gamma V^*(s') \right]
$$

## Q-Value

对于每个状态 $s \in S$，其一个可能动作 $a \in A(s)$ 的质量是：
$$
Q(s,a) = \sum_{s'} P_a(s'|s) \left[ R_a(s'|s) + \gamma V^*(s') \right]
$$

其中 $\gamma$ 是折扣，越接近1，越重视长期奖励，越接近0，越重视短期奖励。

```
0.95, 0.9025, 0.857375, 0.81450625...
0.9, 0.81, 0.729, 0.6561...
0.8, 0.64, 0.512, 0.4096...
0.7, 0.49, 0.343, 0.2401...
```



# Q-Learning

**Input**: MDP $M = \langle S, s_0, A, P_a(s' | s), r(s, a, s') \rangle$ \
**Output**: Q-function $Q$ \
Initialise $Q$ arbitrarily; e.g., $Q(s, a) \leftarrow 0$ for all $s$ and $a$ \
**repeat**\
$\quad$ $s \leftarrow$ the first state in episode $e$\
$\quad$ **repeat** (for each step in episode $e$)\
$\quad\quad$ Select action $a$ to apply in $s$; e.g. using $Q$ and a multi-armed bandit algorithm such as $\epsilon$-greedy\
$\quad\quad$ Execute action $a$ in state $s$\
$\quad\quad$ Observe reward $r$ and new state $s'$\
$\quad\quad$ $\delta \leftarrow r + \gamma \cdot \max_{a'} Q(s', a') - Q(s, a)$\
$\quad\quad$ $Q(s, a) \leftarrow Q(s, a) + \alpha \cdot \delta$\
$\quad\quad$ $s \leftarrow s'$\
$\quad$ **until** $s$ is the last state of episode $e$ (a terminal state)\
**until** $Q$ converges

# SARSA
**Input**: MDP $M = \langle S, s_0, A, P_a(s' | s), r(s, a, s') \rangle$ \
**Output**: Q-function $Q$ \
Initialise $Q$ arbitrarily; e.g., $Q(s, a) \leftarrow 0$ for all $s$ and $a$ \
**repeat**\
$\quad$ $s \leftarrow$ the first state in episode $e$\
$\quad$ Choose $a$ from $s$ using policy derived from $Q$ (e.g., $\epsilon$-greedy)\
$\quad$ **repeat** (for each step in episode $e$)\
$\quad\quad$ Take action $a$, observe $r$, $s'$\
$\quad\quad$ Choose $a'$ from $s'$ using policy derived from $Q$ (e.g., $\epsilon$-greedy)\
$\quad\quad$ $\delta \leftarrow r + \gamma \cdot Q(s', a') - Q(s, a)$\
$\quad\quad$ $Q(s, a) \leftarrow Q(s, a) + \alpha \cdot \delta$\
$\quad\quad$ $s \leftarrow s'$, $a \leftarrow a'$\
$\quad$ **until** $s$ is the last state of episode $e$ (a terminal state)\
**until** $Q$ converges