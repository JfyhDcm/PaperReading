# AUTOMATIC CHAIN OF THOUGHT PROMPTING IN LARGE LANGUAGE MODELS

## Abstract

Chain-of-Thought(CoT) prompting: 为大型语言模型生成中间推理步骤的prompt

CoT prompting有两种模式：

1. **Zero-Shot-CoT**:使用类似“Let's think step by step”去给prompt
2. **Manual CoT:**The other uses a few manual demonstrations(手动演示) one by one, each composed of a question and a reasoning chain that leads to an answer. 

“Diversity”：多样性对于自动构建演示很重要

## Intro

大型语言模型通过在产生答案之前将多步问题分解为中间步骤，在复杂的推理任务中表现出色。

1. *demonstration*: question + reasoning chain（*rationale*“中间推理”：一系列中间推理步骤+预期答案）
2. 去dataset里检索相似问题，然后使用zero-shot-CoT，LLMs仍可能会失败
3. 避免失败的关键是：diversity of demonstration questions

Auto-CoT:

1. 首先，将数据集问题划分为几个不同的clusters。
2. 其次，从每个聚类中选择一个具有代表性的问题，并使用简单的启发式Zero-Shot-CoT生成其推理链。

## Challenge of Auto-CoT

**Retrieaval-Q-CoT**: 通过计算Sentence-BERT的sentence embedding， 然后计算cosine similarity选取top-k 

**Random-Q-CoT**:随机抽取k个

1. 在算术数据集上（arithmetic dataset），出人意料的是，Random-Q-CoT效果要优于Retrieval-Q-CoT【我认为可能是diversity更有用，数学是一种需要泛化的抽象思想，某种角度说明了学好数学要多做题。。。】

2. Retrieval-Q-CoT is effective when human annotations are available.

![image-20221222230946004](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221222230946004.png)

### Retrieval-Q-CoT Fails due to Misleading by Similarity

Misleading by similarity: zero-shot使用的example的答案（或label）是直接生成的，可能会有错误，所以使用错误的example进行prompt会造成错误传播。

600个问题中，zero-shot造成错误的有128个。即128/600=21.3%。

如果经过Retrieval-Q-CoT或Random-Q-CoT仍然回答错误的，我们称为*unresolved question*。

那么当一个方法的unresolved rate更高，说明其方法更错误传播。这里Retrieval方法就是如此。

![image-20221222233708906](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221222233708906.png)

### Errors Frequently Fall into the Same Cluster

![image-20221223114814167](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221223114814167.png)

从图中可以看到，CLuster2的错误率非常之高。可能因为LLM的zero-shot缺少解决该种问题的技能。

我们称此类为*frequent-error cluster*

### Diversity May Mitigate Misleading by Similarity

prompt中的一小部分错误（8个prompt中有1-2个错误），并不会损害测试问题的整体推理表现。

Auto-CoT：

1. 减少了基于相似性带来的错误传递，通过diversity，因为错误的一般属于一个cluster
2. 让模型学会了更多的技能，从更多的diversity里

对于那小部分错误，可以使用启发式的方法来将其剔除。比如生成更长答案的一般是错误的。

## Auto-CoT: Automatic Chain-of-Thought Prompting

选择的标准是：rationale推理过程不超过60token，并且不超过5个推理步骤。

## Experiment

![image-20221223142331796](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221223142331796.png)

![image-20221223143038959](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221223143038959.png)

## Else

1. demonstration是一个triple，由<question, rationale, answer>组成。

2. 错误的zero-shot也是有用的，它的逻辑是正确的，虽然它答案是错的。

3. 失败的zero-shot是因为缺少了一定的skill

   ![image-20221225134739066](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221225134739066.png)

