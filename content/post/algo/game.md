---
date: "2024-05-30T11:13:45+10:00"
draft: false
title: "Game Theory"
categories:
    - COMP90054
tags: ["algorithm"]
params:
  math: true
---


- pure Strategy: single action
- mixed Strategy: probability distribution over actions
- weakly dominate: $\leq$
- strongly dominate: $<$
- a weakly(strictly) dominant strategy: always better than any other strategy
- nash equilibrium: 每个agent都选了最优策略，其他agent不会改变策略

- indifference: 通过调整我的策略概率，改变对手的收益（payoff）期望，使无论对手如何选择，他的满意度（utility）都一样


## Utility Function

U_i(a): what can agent i get from action a


## Normal Form Game

一轮，不知道对手的策略，只知道对手的utility function

## Extensive Form Game 广义形式博弈

轮流决策，所以知道对手的策略

## Subgame Perfect Equilibrium 子博弈完美均衡

当前玩家在他的回合的最优策略，对手在他的回合的最优策略。。。

## Backward Induction 反向归纳
```
输入：广义形式博弈 G = (N, Agt, S, s_0, A, T, r)
输出：每个状态 s ∈ S 的子博弈均衡

函数 BackwardInduction(s ∈ S):
    如果 A(s) = ∅，则返回 r(s)
    best_child ← (-∞, ..., -∞)
    对于每个 a ∈ A(s)：
        s' ← T(s,a)
        child_reward ← BackwardInduction(s')
        如果 child_reward(P(s)) > best_child(P(s))，则 best_child ← child_reward
    返回 best_child

返回 BackwardInduction(s_0)
```

## Multi-agent Q-learning

```
输入：随机博弈 G = (S, s_0, A^1, ..., A^n, r^1, ..., r^n, Agt, P, γ)
输出：Q函数 Q^j，其中 j 是 self agent

初始化 Q^j 任意，例如，对于所有的状态 s 和联合动作 a，Q^j(s,a)=0

重复：
    s ← episode e 的第一个状态
    重复（对于 episode e 的每一步）：
        选择在 s 中应用的动作 a^j
            例如，使用 Q^j 和一个多臂老虎机算法，如 ε-greedy
        在状态 s 中执行动作 a^j
        观察奖励 r^j 和新状态 s'
        Q^j(s,a) ← Q^j(s,a) + α * [r^j + γ * max_a' Q^j(s',a') - Q^j(s,a)]
        s ← s'
    直到 episode e 结束（一个终止状态）
直到 Q 收敛
```