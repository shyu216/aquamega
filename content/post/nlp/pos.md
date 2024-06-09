---
date: "2024-05-28T03:56:05+10:00"
draft: false
title: "Part-of-Speech Tagging"
categories:
    - COMP90042
tags: ["NLP", "AI"]
params:
  math: true
---

## Part-of-Speech(词类)


Colourless green ideas sleep furiously.

- Open Classes (Content Words)
    - Noun
    - Verb
    - Adjective
    - Adverb
- Closed Classes (Function Words) (Fixed number of words)
    - Preposition
    - Determiner
    - Pronoun
    - Conjunction
    - Interjection

Ambiguity: A word can have multiple meanings. A sentence can have multiple interpretations.


在自然语言处理（NLP）中，POS代表词性标注（Part-of-Speech Tagging）。词性标注是一种将每个词语与其语法范畴（即词性）相关联的过程。它是NLP中的一项基本任务，用于确定句子中每个单词的词类。

常见的词性包括名词、动词、形容词、副词、介词、代词、冠词、连词等。通过进行词性标注，可以帮助计算机理解句子的结构和含义，为其他NLP任务（如句法分析、语义分析和机器翻译等）提供基础。

以下是一个例子，展示了一句英文句子的词性标注示例：

句子：I love eating ice cream.  
词性标注：PRON VERB VERB NOUN NOUN.

在这个例子中，"I"被标注为代词（PRON），"love"和"eating"被标注为动词（VERB），"ice"和"cream"被标注为名词（NOUN）。

词性标注可以通过使用基于规则的方法、基于统计的机器学习方法（如隐马尔可夫模型）或基于深度学习的方法（如循环神经网络和转换器模型）来实现。这个任务在NLP中具有广泛的应用，对于许多文本处理任务都是重要的预处理步骤。

- NN（noun）名词：cat（猫）、book（书）、table（桌子）
- VB（verb）动词：run（跑）、eat（吃）、sleep（睡觉）
- JJ（adjective）形容词：big（大的）、happy（快乐的）、red（红色的）
- RB（adverb）副词：quickly（快速地）、well（好地）、very（非常）
- DT（determiner）限定词：the（定冠词）、this（这个）、some（一些）
- CD（cardinal number）基数词：one（一）、three（三）、ten（十）
- IN（preposition）介词：on（在...上）、with（和...一起）、at（在...处）
- PRP（personal pronoun）人称代词：I（我）、you（你）、he（他）
- MD（modal）情态动词：can（能够）、should（应该）、will（将会）
- CC（coordinating conjunction）并列连词：and（和）、but（但是）、or（或者）
- RP（particle）小品词：up（向上）、down（向下）、out（出去）
- WH（wh-pronoun）疑问代词：who（谁）、what（什么）、which（哪个）
- TO（to）不定式标记：to（去）、to（为了）、to（到）


## Penn Treebank 词性标记集

Penn Treebank 的词性标注集（POS tagset）是一种广泛使用的英文词性标注方法。

- `CC`：并列连词 (Coordinating conjunction)
- `CD`：基数词 (Cardinal number)
- `DT`：限定词 (Determiner)
- `EX`：存在句引导词 (Existential there)
- `FW`：外来词 (Foreign word)
- `IN`：介词或从属连词 (Preposition or subordinating conjunction)
- `JJ`：形容词 (Adjective)
- `JJR`：比较级形容词 (Adjective, comparative)
- `JJS`：最高级形容词 (Adjective, superlative)
- `LS`：列表项标记 (List item marker)
- `MD`：情态动词 (Modal)
- `NN`：名词, 单数或集数 (Noun, singular or mass)
- `NNS`：名词, 复数 (Noun, plural)
- `NNP`：专有名词, 单数 (Proper noun, singular)
- `NNPS`：专有名词, 复数 (Proper noun, plural)
- `PDT`：前限定词 (Predeterminer)
- `POS`：所有格结束 (Possessive ending)
- `PRP`：人称代词 (Personal pronoun)
- `PRP$`：所有格代词 (Possessive pronoun)
- `RB`：副词 (Adverb)
- `RBR`：副词, 比较级 (Adverb, comparative)
- `RBS`：副词, 最高级 (Adverb, superlative)
- `RP`：小品词 (Particle)
- `SYM`：符号 (Symbol)
- `TO`：to
- `UH`：感叹词 (Interjection)
- `VB`：动词, 原形 (Verb, base form)
- `VBD`：动词, 过去式 (Verb, past tense)
- `VBG`：动词, 现在分词或动名词 (Verb, gerund or present participle)
- `VBN`：动词, 过去分词 (Verb, past participle)
- `VBP`：动词, 非第三人称单数现在式 (Verb, non-3rd person singular present)
- `VBZ`：动词, 第三人称单数现在式 (Verb, 3rd person singular present)
- `WDT`：wh-限定词 (Wh-determiner)
- `WP`：wh-代词 (Wh-pronoun)
- `WP$`：wh-所有格代词 (Wh-pronoun, possessive)
- `WRB`：wh-副词 (Wh-adverb)