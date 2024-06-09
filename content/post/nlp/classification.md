---
date: "2024-05-27T02:56:05+10:00"
draft: false
title: "Text Classification"
categories:
    - COMP90042
tags: ["NLP", "AI"]
params:
  math: true
---


- Topic classification
- Sentiment analysis
- Native language identification
- Natual language inference
- Automatic fact-checking
- Paraphrase


## Topic Classification

- Motivation: library science, information retrieval, etc.
- Classes: topic categories
- Features: bag-of-words, n-grams, etc.
- Corpus: reuters news corpus, pubmed abstracts, tweets with hashtags

## Sentiment Analysis

- Motivation: opinion mining, business analytics
- Classes: positive, negative, neutral
- Features: n-grams, polarity lexicons, etc.
- Corpus: movie reviews, SEMEVAL twitter polarity dataset

## Native Language Identification

- Motivation: forensic linguistics, educational applications
- Classes: native languages
- Features: character n-grams, syntactic features (POS), phonological features
- Corpus: TOEFL/IELTS essays

## Natural Language Inference (textual entailment 文本蕴含)

- Motivation: language understanding
- Classes: entailment, contradiction, neutral
- Features: word overlap, length difference, etc.
- Corpus: SNLI, MultiNLI

## Build a Text Classifier

1. Identify the task
2. Collect and preprocess data
3. Annotation
4. Select features
5. Select an algorithm
6. Train and tune the model
7. Evaluate the model

## Naive Bayes Classifier

assume independence between features

$$P(c|d) = \frac{P(d|c)P(c)}{P(d)}$$

Pros:
- Fast, simple
- Robust, low-variance
- Optimal if independence holds

Cons:
- Rarely holds
- Low accuracy
- Smoothing needed for unseen

## Logistic Regression

$$P(c|d) = \frac{1}{1 + e^{-\sum_{i=1}^n w_i x_i}}$$

Pros:
- Better performance

Cons:
- Slow
- Scaling needed
- Regularization needed for overfitting

## Support Vector Machine

To find the hyperplane that maximizes the margin

Pros:
- Fast and accurate
- Non-linear kernel
- Work well in big data

Cons:
- Multi-class classification
- Scaling needed
- Imbalanced data
- Interpretability

## K-Nearest Neighbors

Euclidean distance, cosine similarity

Probs:
- Simple
- No training needed
- Multi-class classification
- Optimal with infinite data

Cons:
- Set k
- Imbalanced classes
- Slow

## Decision Tree

Greedy maxmize information gain

Pros:
- Fast
- Non-linear
- Good for small data
- Feature scaling irrelevant

Cons:
- Not that interpretable
- Redundant features
- Not competitive for big data

## Random Forest

Pros:
- Better than decision tree
- Parallelizable

Cons:
- Same as decision tree

## Neural Network

Pros:
- Powerful

Cons:
- Hyperparameters
- Training time
- Overfitting

## Evaluation

- Accuracy

    $$\frac{TP + TN}{TP + TN + FP + FN}$$

- Precision
    
    $$\frac{TP}{TP + FP}$$

- Recall
    
    $$\frac{TP}{TP + FN}$$  

- F1-score
    
    $$\frac{2 \times \text{precision} \times \text{recall}}{\text{precision} + \text{recall}}$$


