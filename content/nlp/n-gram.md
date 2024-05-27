---
date: "2024-05-27T14:56:05+10:00"
draft: false
title: "N-gram Language Model"
tags: ["comp90042", "nlp"]
categories: ["nlp"]
params:
  math: true
---

# Language Model

To explain language, based on probability, for generation.

- Query completion(搜索引擎)
- Optical character recognition(OCR)
- Translation

## N-gram

$$P(w_1, w_2, \cdots, w_n) = P(w_1)P(w_2|w_1)P(w_3|w_1, w_2) \cdots P(w_n|w_1, w_2, \cdots, w_{n-1})$$

- Maximum Likelihood Estimation

$$P(w_i|w_{i-1}) = \frac{C(w_{i-1}, w_i)}{C(w_{i-1})}$$

Use special tags to denote the beginning and end of a sentence, i.e. `<s>`, `</s>`.

## Smoothing

Handle unseen words.

- Laplacian (add-one) smoothing

    $P(w_i|w_{i-1}) = \frac{C(w_{i-1}, w_i) + 1}{C(w_{i-1}) + V}$

- Add-k smoothing

    $P(w_i|w_{i-1}) = \frac{C(w_{i-1}, w_i) + k}{C(w_{i-1}) + kV}$

- Lidstone smoothing (Generalized Add-k)

- Absolute discounting (Borrow a bit of probability mass from seen words to unseen words)

- Backoff (Use lower-order n-gram)

- Knser-Ney (Versatility of lower-order n-gram), co-occur with many words

- Interpolation (Combine lower-order n-gram)