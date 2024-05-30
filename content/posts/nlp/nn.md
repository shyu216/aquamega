---
date: "2024-05-28T14:56:05+10:00"
draft: false
title: "Neual Networks"
tags: ["comp90042", "nlp"]
categories: ["nlp"]
params:
  math: true
---


# 非线性激活函数是神经网络中的关键组成部分，它可以帮助神经网络学习和逼近复杂的模式。非线性激活函数的主要目的是将输入信号转换为输出信号，但它不仅仅是复制输入到输出。它会修改或者变换输入的方式，使得可以适应网络的需要。

常见的非线性激活函数包括：

- ReLU（Rectified Linear Unit）：这是最常用的激活函数，它将所有负值设为0，正值保持不变。

- Sigmoid：这个函数将任何数值都映射到0和1之间，它在早期的神经网络中非常流行，但现在已经较少使用，因为它在输入值很大或很小的时候，梯度几乎为0，这会导致梯度消失问题。

- Tanh（Hyperbolic Tangent）：这个函数将任何数值都映射到-1和1之间，它比sigmoid函数的输出范围更广，因此在某些情况下，它的性能比sigmoid函数更好。

- Softmax：这个函数通常用在神经网络的输出层，特别是在处理多分类问题时。它可以将一组数值转换为概率分布。


# Regularization 正则化

- L1 Norm
- L2 Norm
- Dropout