---
date: "2024-05-28T00:56:05+10:00"
draft: false
title: "Neual Networks"
tags: ["comp90042", "nlp"]
params:
  math: true
---


神经网络（Neural Network）是一种模拟人脑神经元工作方式的机器学习模型。它由大量的神经元（也称为节点或单元）组成，这些神经元按照一定的层次结构排列，包括输入层、隐藏层和输出层。

每个神经元接收来自上一层神经元的输入，然后通过一个激活函数（如 Sigmoid、ReLU 等）处理这些输入，得到一个输出，这个输出再传递给下一层的神经元。

神经网络的训练通常使用反向传播（Backpropagation）算法和梯度下降（Gradient Descent）算法。在训练过程中，神经网络通过不断调整神经元之间的连接权重，来最小化预测值和真实值之间的差异。

神经网络可以处理非线性问题，适用于各种复杂的机器学习任务，如图像识别、语音识别、自然语言处理等。但是，神经网络的训练需要大量的数据和计算资源，而且模型的解释性较差，这是它的一些挑战。

A Neural Network is a machine learning model that simulates the way neurons in the human brain work. It consists of a large number of neurons (also known as nodes or units) arranged in a certain hierarchical structure, including input layers, hidden layers, and output layers.

Each neuron receives input from the neurons in the previous layer, then processes these inputs through an activation function (such as Sigmoid, ReLU, etc.) to produce an output, which is then passed on to the neurons in the next layer.

Neural networks are typically trained using the Backpropagation algorithm and the Gradient Descent algorithm. During training, the neural network minimizes the difference between the predicted values and the actual values by continuously adjusting the connection weights between neurons.

Neural networks can handle non-linear problems and are suitable for various complex machine learning tasks, such as image recognition, speech recognition, natural language processing, etc. However, the training of neural networks requires a large amount of data and computational resources, and the interpretability of the model is relatively poor, which are some of the challenges.

# 前馈神经网络
前馈神经网络是一种基础的神经网络，信息只在一个方向上流动，从输入层到输出层。

1. 任务：
  1. 主题分类：使用神经网络对文本或其他数据进行主题分类。
  2. 语言模型：使用神经网络来理解和生成语言。
  3. 词性标注：使用神经网络来识别文本中每个词的词性。

2. 词嵌入：一种表示词汇的技术，将词汇映射到向量空间，使得语义相近的词汇在向量空间中的距离也相近。
3. 卷积网络：一种特殊的神经网络，特别适合处理网格形式的数据，如图像。

# 循环神经网络
循环神经网络是一种可以处理序列数据的神经网络，它可以利用前面的信息来影响后面的输出。
1. RNN语言模型：使用循环神经网络来理解和生成语言，特别适合处理文本等序列数据。
2. LSTM：
   1. 门的功能：LSTM是一种特殊的RNN，它有三个门（输入门、遗忘门和输出门）来控制信息的流动。
   2. 变体：LSTM有多种变体，如GRU（门控循环单元），它简化了LSTM的结构。
3. 任务：
   1. 文本分类：情感分析：使用RNN进行文本分类，如情感分析，判断文本的情感倾向。
   2. 词性标注：使用RNN来识别文本中每个词的词性。

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

# LSTM

- Memory cell：记忆单元，用来存储信息
- Hidden state：隐藏状态，用来传递信息
- Forget gate：遗忘门，用来控制记忆单元中的信息是否被遗忘
- Input gate：输入门，用来控制新的信息是否被存储到记忆单元中
- Output gate：输出门，用来控制隐藏状态中的信息是否被传递到下一个时间步