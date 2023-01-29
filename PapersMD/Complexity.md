# COMPLEXITY-BASED PROMPTING   FOR MULTI-STEP REASONING

## Abstract

higher reasoning complexity i.e. chains with more reasoning step 的prompt更好

## Intro

1. few-shot prompt比传统的fine-tune更加sample efficient
2. CoT、表达推理过程短句子在数学应用题方面体现了很强的推理能力
3. prompt select相关的就是prompt答案的标注；如果答案很好获得，那么什么是性能最好的prompt；如果答案不好获得，那么应该标注哪些个问题来获得最好的prompt
4. complexity-based 可以认为来自self-consistency（自洽性）
5.  A careful analysis shows that the number of reasoning steps is the most prominent factor, over confounders like prompt lengths or the number of input cases. 一个谨慎的分析认为推理的步数大过prompt长度或者输入case数等因素

## Related Work

### Emergent Abilities and Multi-step Reasoning

Unique skill (AKA Emergent Ability): When the model parameters is over 100B, 突然掌握了reasoning的能力

Multi-step Reasoning的两个特点：

1. 这是一个LLM表现远超过small model的任务，例如文本分类任务，LLM和小模型表现相差不多
2. 这个任务上few-shot prompt LLM表现远超过full dataset fine-tune的small model甚至large model

### Chain of Thoughts Reasoning

1. Reasoning Ability 只能通过 chain of thoughts 来引出
2. CoT效果的提升可以通过 self-consistency、用latex格式的数据来预训练模型、context selection（上下文选择）、添加一些神奇的短语比如“Let's think step by step”

### Example Selection for Prompting

1. The difficulty is that it is extremely hard to extract generalizable regularity from empirical observations that can form effective selection criteria. 困难在于，从经验观察中提取可归纳的规律性，从而形成有效的选择标准是极其困难的。

## Relation to Classical Semantic Parsing

Semantic Parsing：把一个自然语言的utterance转化为逻辑格式（机器可以理解的形式）。

CoT和classical semantic parsing很像：都是生成一个逻辑形式，然后再数据库上执行这个形式以获得答案。抽样然后投票的做法也类似于将语义解析边缘化（marginalizating out semantic parses）。

还有把in-context learning与classical贝叶斯 link起来的论文

## Complexity-Based Prompting

1. 论文假设使用更复杂的sample效果更好，理由是复杂的sample包含了更多简单的sample。
2. 这里的“复杂”指的是中间推理的步骤数，这个指标与*问题长度、公式长度*是一致的。
3. 模型会*shortcut*来生成答案，因为训练数据中有不可避免的虚假相关性。
4. 对于生成很多答案投票的方式，本文采用选取其中最复杂的Top-K个答案进行投票，这样准确率更高，被称为“Complexity-based Consistency”。相反地，用最简单的Top-K，准确率会大大下降。

## Experiment

数据集：GSM8K、MultiArith、MathQA

复杂提示可以帮助完成简单问题，但是简单提示不能帮助完成

## Analysis

1. 当问题没有annotation时，可以使用问题长度或者公式长度来代表complexity
2. prompt中的分隔器的研究比如"\n","."等，包括更适合中间推理步骤的“step.i”等，结果如下：![image-20230128113705644](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20230128113705644.png)
3. 





















