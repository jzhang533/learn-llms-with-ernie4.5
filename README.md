# 通过文心 4.5 学习大语言模型

## 授课记录

- [2025-9 记录](./course_offerings/202509_offering.md)

## 课程大纲

### 第一章：大语言模型概述

**课件：** [大语言模型概述](https://www.canva.cn/design/DAGvFYm0hPY/RQ7A7y3T-BtjsrryGP9kHA/view?utm_content=DAGvFYm0hPY&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h8a1b76d4e2)

**学习目标：**

- 学会什么是大语言模型。
- 大语言模型的组成模块。
- 了解常见的大语言模型的类型。
- 了解大语言模型的解码器。
- 大语言模型发展历史科普。

**课后练习：**

- 给定一句话，如：“hello, world”，用 ernie4.5-0.3b 模型计算这句话的概率。
- ernie4.5-0.3b 的 base model 和 instruct model 分别计算这句话的概率，哪个概率高？为什么？
- **进阶：** 自己实现一个 greedy search 解码器，自己的解码器的输出结果，跟调用 API 输出的结果一致。

### 第二章：分词与词向量

**课件：** [分词与词向量](https://www.canva.cn/design/DAGv8rCIe-8/rZ-oVX2YcOGObX1EBXa3jg/view?utm_content=DAGv8rCIe-8&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h22674801ac)

**学习目标：**

- 了解 tokenizer 的功能和作用。
- 了解常见的 tokeninzer 的类型。
- 了解 special token 起到的作用。
- 掌握 embedding 的基本知识，类型，以及在 LLM 中所起到的作用。
- 掌握如何训练出来 embedding。

**课后练习：**

- 使用 ernie4.5-0.3b 模型的 tokenizer 输出两个给定的 token 对应的 id 。
- ernie4.5-0.3b  模型的字典的大小是多少？embedding 层的大小是多少？
- 给定两个 token，仅用 ernie4.5-0.3b 模型的 embedding 层，计算这两个 token 的相似度（hint：使用 cosine）。
- **进阶：** 给定两句话，仅用 ernie4.5-0.3b 模型的 embedding 层，计算这两句话的相似度。
- **进阶：** 仅用 ernie4.5-0.3b 模型的 embedding 层和 LM Head（即：删除所有的 transformer block ），使用第一章自己设计的 greedy search 解码器，让模型也可以生成文本呢。

### 第三章：注意力机制与 Transformer 结构

**课件：** [注意力机制与 Transformer 结构](https://www.canva.cn/design/DAGwroOgcHw/b148P5koMVsKnIWgmAH4zg/view?utm_content=DAGwroOgcHw&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h00d022d771)

**学习目标：**

- 了解 encoder-decoder 结构。
- 了解引入 attention 机制的原因，以及常见的 attention 的类型。
- 掌握 MHA 结构里的详细计算公式，并学会如何计算 MHA 里的模型参数数量。
- 了解常见 NLP 任务类型：分类、机器翻译、Fill-Mask、文本生成。

**课后练习：**

- ernie4.5-0.3b, ernie4.5-21b-a3b, ernie4.5-300b-a47b 分别都有多少层的 transformer block ？
- 去掉 transformer block 中的 attention 模块后，模型是什么样的语言模型（A：unigram, B：bigram; C：trigram；D：condtioned on previous tokens ）。
- 为什么 transformer 结构可以并行化，而 RNN/LSTM 不行？
- 使用一个 encoder-only 模型（hint: BERT or ERNIE 3.0）计算给定的输入（如："巴黎是[MASK]的首都"，模型预测出的前 5 个 token 是什么，对应的概率是多少？
- 使用 ernie4.5-0.3b 模型，给定一句话（如："I have a dream"），计算在当前（token（如："dream"）下，这句话中的每个 token 用第 0 个 head 上 计算出的 attention weight 是多少？
- **进阶：** 仅保留 ernie4.5-0.3b-base 模型的 embedding 层和第一个 transformer block 层（Ernie4_5DecoderLayer），然后接一个可以进行二分类的 head，自己构造 10 条情感分类的数据集，训练这个改造后的模型，让它可以 overfit 你的这个数据集。
- **进阶：** 用 encoder-decoder 模型结构从头训练一个机器翻译模型。（使用这个数据集：<https://www.manythings.org/anki/>）（hint：设计一个比较小的模型结构，这样在本地的 CPU 机器上就可以训出来）

### 第四章：大语言模型的最新进展

**课件：** 大语言模型的最新进展

**学习目标：**

- 了解 ernie4.5-0.3b 模型的模型结构跟最早的 transformer block 结构相比的变化（GQA, RoPE，RMSNorm）。
- 了解 MoE 模型结构（通过 ERNIE4.5-21b 及 ERNIE4.5-300B）。
- 了解 Reasoning Model 的概要进展。
- 了解多模态模型的概要进展（通过 ERNIE4.5-VL）。

**课后练习：**

- 计算出 ernie4.5-0.3b 模型的总的参数数量，精确到个位数。
- MoE 模型结构是对 transformer block 中的哪个部分的改进？
- 文心 4.5 多模态模型里的视觉部分的表示学习用的是什么模型结构？
- **进阶：** 使用 ernie4.5-0.3b-base 的模型结构，但是把参数规模缩减到万分之一左右（即：总参数只有 30 万）。在一个小的数据集上（如汪峰的歌词数据），训练出来一个非常小的跟 ernie4.5-0.3b 的模型结构一致的语言模型，可以生成文本（如：随机生成汪峰的歌）。

### 第五章：后训练与微调

**课件：** 大语言模型的后训练

**学习目标：**

- 了解有监督微调 (SFT)、直接偏好优化 (DPO) 和在线强化学习 (Online Reinforcement Learning) 等训练后方法。
- 了解 SFT、DPO 两种训练后方法的基本概念、它们的常见使用场景和如何准备数据。
- 掌握使用 erniekit 把一个 base model 通过 SFT/DPO 阶段得到一个 instruct model 的实践

**课后练习：**

- SFT 适用的场景是？
- DPO 适用的场景是？
- **进阶：** 使用 ernie4.5-0.3b 模型训练通过 DPO 训练一个有自我认知的后训练模型。
