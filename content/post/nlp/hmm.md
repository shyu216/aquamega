---
date: 2024-05-27
draft: false
title: "Hidden Markov Model"
categories:
    - COMP90042
tags: 
    - NLP
    - AI
---

- w：word
- t：tag
- emission probability: $P(w|t)$ 从tag到word的概率
- transition probability: $P(t|t')$ 从上一个tag到当前tag的概率


## Viterbi Algorithm

从最开始算起，每个tag的概率是由前一个tag的概率和从前一个tag到当前tag的概率相乘得到的。

$\hat{t} = \arg\max_{t} \prod_{i=1}^{n} P(w_i|t)P(t|t')$, $t'$是前一个tag, $\hat{t}$是当前的估计值。


## Generative vs Discriminative Tagger

- HMM是generative model，可以用来生成数据，无监督的学习。
- discriminative model例如CRF，需要有监督的数据，可以学到更丰富的特征，大多数deep learning的模型都是discriminative model。