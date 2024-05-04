---
date: "2024-05-02T11:13:45+10:00"
draft: false
title: "Hill Climbing"
tags: ["comp90054"]
params:
  math: true
---


# 爬山算法

- σ := make-root-node(init())
- 永远执行以下操作：
    - 如果 is-goal(state(σ))：
        - 返回 extract-solution(σ)
    - Σ′ := {make-node(σ,a,s′) |(a,s′) ∈succ(state(σ)) }
    - σ := 选择 Σ′ 中 h 值最小的元素 /* （随机打破平局） */