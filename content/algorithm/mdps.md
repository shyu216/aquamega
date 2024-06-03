---
date: "2024-05-02T11:13:45+10:00"
draft: false
title: "MDPs"
tags: ["comp90054", "algo"]
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

$
V^*(s) = \max_{a \in A(s)} \sum_{s'} P_a(s'|s) \left[ R_a(s'|s) + \gamma V^*(s') \right]
$


- 所有可能的下一个状态的概率
- 动作的奖励
- 下一个状态的价值 x 折扣，前一个iteration存储的价值

## Q-Value

对于每个状态 $s \in S$，其一个可能动作 $a \in A(s)$ 的质量是：\
$
Q(s,a) = \sum_{s'} P_a(s'|s) \left[ R_a(s'|s) + \gamma V^*(s') \right]
$

其中 $\gamma$ 是折扣，越接近1，越重视长期奖励，越接近0，越重视短期奖励。

```
0.95, 0.9025, 0.857375, 0.81450625...
0.9, 0.81, 0.729, 0.6561...
0.8, 0.64, 0.512, 0.4096...
0.7, 0.49, 0.343, 0.2401...
```

## Policy

$\pi(s) = arg max Q(s,a)$

# Multi-Armed Bandit

平行地尝试多个动作，平衡exploitation和exploration。

- minimising regret，没有选择最佳动作的损失

    **输入**: 多臂老虎机问题 $M = \{X_{i,k}, A, T\}$ \
    **输出**: Q函数 $Q$ \
    初始化 $Q$ 为任意值; 例如，对所有的臂 $a$，$Q(a) \leftarrow 0$ \
    初始化 $N$ 为任意值; 例如，对所有的臂 $a$，$N(a) \leftarrow 0$ \
    $k \leftarrow 1$ \
    **while** $k \leq T$ **do**\
    $\quad$ $a \leftarrow$ 在第 $k$ 轮选择一个臂\
    $\quad$ 在第 $k$ 轮执行臂 $a$ 并观察奖励 $X_{a,k}$\
    $\quad$ $N(a) \leftarrow N(a) + 1$\
    $\quad$ $Q(a) \leftarrow Q(a) + \frac{1}{N(a)} [X_{a,k} - Q(a)]$\
    $\quad$ $k \leftarrow k + 1$\
    **end while**

- $\epsilon$-greedy，以 $1-\epsilon$ 的概率选择最佳动作，以 $\epsilon$ 的概率选择随机动作

- $\epsilon$-greedy with decay，随着时间的推移，减少 $\epsilon$ 的值

- UCB 

    $\text{argmax}_{a}\left(Q(a)   +   \sqrt{\frac{2 \ln t}{N(a)}}\right)$

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


- $max_{a'} Q(s', a')$ 也可以写成 $V(s')$，即下一个状态的价值

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


- Q-Learning是off-policy，因为on当前策略下的Q值，对当前策略更乐观
- SARSA是on-policy，所以off了当前策略下的Q值，更保守

# n-step reinforcement learning

记账，在n-step后再一起更新Q值。

# MCTS

- Selection：选择一个节点，直到找到一个未扩展的节点
- Expansion：扩展一个未扩展的节点
- Simulation：模拟一个随机游戏，直到结束
- Backpropagation：更新所有访问的节点的值

offline：完成所有模拟后再选择最佳动作

online：每次模拟后选择最佳动作，继续对新的节点进行模拟。在下次选择时，同时也利用了之前的模拟结果，MCTS是online的。


用平均值更新：新Q = 旧Q + 学习率 * 误差，实际上就是平均值

# UCT

用UCB来select。

$\text{argmax}_{a \in A(s)} Q(s,a) + 2 C_p \sqrt{\frac{2 \ln N(s)}{N(s,a)}}$ \
where $C_p$ 自己选，看是更偏向exploration还是exploitation


# Linear Q-functionn Approximation

\# features = \# states * \# actions

$Q(s,a) = f^T w = \sum_{i=1}^{n} f_i(s,a) w_i$

## Update 
$w \leftarrow w + \alpha \delta f(s,a)$ \
where \
$\delta = r + \gamma \max_{a'} Q(s',a') - Q(s,a)$ if Q-learning \
$\delta = r + \gamma Q(s',a') - Q(s,a)$ if SARSA


# Shaped Reward

$Q(s,a) \leftarrow Q(s,a) + \alpha [r + \underbrace{F(s,s')}_{\text{additional reward}} + \gamma \max_{a'} Q(s',a') - Q(s,a)]$

## Potential-based Reward Shaping

$F(s,s') = \gamma \Phi(s') - \Phi(s)$

For example, in Gridworld, \
$\Phi(s) = 1 - \frac{|x(g) - x(s)| + |y(g) - y(s)|}{width + height - 2}$

# Policy Iteration

魔改bellman方程，将所有动作可能性替换成当前策略下的动作。