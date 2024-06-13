---
date: 2024-05-27
draft: false
title: "Preprocessing"
categories:
    - COMP90042
tags: 
    - NLP
    - AI
---

## Preprocessing

- Word
- Sentence: words
- Document: sentences
- Corpus: documents
- Word Token: word instance
- Word Type: verb, noun, etc.
- Lexicon: word types


## Steps
1. Remove unwnated formatting, i.e. HTML tags
2. Sentecne segmentation, break text into sentences
3. Tokenization, break sentences into words
4. Normalization, transform words into canonical form, i.e. lower case
5. Stopword removal, delete unwanted words, i.e., "the", "I", ".", etc.

### Max Match Algorithm

Greedily match the longest word in the dictionary. Used in the language withoout space between words, i.e. Chinese.

### Byte Pair Encoding

Iteratively merge the most frequent pair of bytes. Used in ChatGPT.

Adv:
- Data-informed tokenization
- Works for different languages
- Deals better with unknown words


Disadv:
- Rarer words will be split into subwords, even individual letter


### Word Normalization

Goal: reduce vocabulary size, map different forms of a word to the same form

形态处理（Morphological processing）通常包括词干提取（stemming）和词形还原（lemmatization）

- Lowercasing
- Remove morphology, i.e. "running" -> "run"
- Correct spelling, i.e. "colour" -> "color"
- Expand abbreviations, i.e. "can't" -> "cannot"

### Inflectional Morphology(屈折形态)

It creates grammatical variants of a word, i.e. "run" -> "running", "ran", "runs"

Nouns, verbs, adjectives, adverbs...

### Lemmatization(词形还原)

To remove inflection. 

Lemma(词元): the uninflated form

### Derivational Morphology(派生形态)

It creates new words.

- Change the lexical category(), i.e. "happy" -> "happiness"
- Change the meaning, i.e. "happy" -> "unhappy"

### Stemmization(词干提取)

To remove derivation.

Stem(词干): the root form

### The Porter Stemmer

most widely used in English

- C: consonant(辅音)
- V: vowel(元音)
- m: measure $[C](VC)^m[V]$

### Stopword Removal

Typically in bag-of-words model

All closed-class or function words, any high frequency words
