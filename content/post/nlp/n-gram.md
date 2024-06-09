---
date: "2024-05-27T01:56:05+10:00"
draft: false
title: "N-gram Language Model"
categories:
    - COMP90042
tags: ["NLP", "AI"]
params:
  math: true
---

## Language Model

To explain language, based on probability, for generation.

- Query completion(搜索引擎)
- Optical character recognition(OCR)
- Translation

### N-gram

$$P(w_1, w_2, \cdots, w_n) = P(w_1)P(w_2|w_1)P(w_3|w_1, w_2) \cdots P(w_n|w_1, w_2, \cdots, w_{n-1})$$

- Maximum Likelihood Estimation

$$P(w_i|w_{i-1}) = \frac{C(w_{i-1}, w_i)}{C(w_{i-1})}$$

Use special tags to denote the beginning and end of a sentence, i.e. `<s>`, `</s>`.

### Smoothing

Handle unseen words.

- Laplacian (add-one) smoothing

    $P(w_i|w_{i-1}) = \frac{C(w_{i-1}, w_i) + 1}{C(w_{i-1}) + V}$

- Add-k smoothing

    $P(w_i|w_{i-1}) = \frac{C(w_{i-1}, w_i) + k}{C(w_{i-1}) + kV}$

- Lidstone smoothing 
  - Generalized Add-k, 所有非负实数

- Absolute discounting 
  - Borrow a bit of probability mass from seen words to unseen words， 每个借一点，均摊给没见过的词

- Katz Backoff 
  - Use lower-order n-gram
  - Issue：低阶n-gram可能有很高概率，但此n-gram组合显然不会存在

- Knser-Ney 
  - Versatility of lower-order n-gram, co-occur with many words
  - 让更通用的低阶n-gram有更高的概率
  - contiuation probability $P_{cont}(w_i) = \frac{|{w_{i-1}:C(w_{i-1}, w_i) > 0}|}{\sum_{w_i}C(w_{i-1}, w_i)}$
- Interpolation 
  - Combine lower-order n-gram
  - 给不同阶的n-gram加权，相加