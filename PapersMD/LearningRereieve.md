# Learning To Retrieve Prompts for In-Context Learning

## Abstract

1. In-context learning是NLU任务的一种，很依赖于prompt的选择（termed prompts）

## Intro

1. Prompt Retrieval的两种办法：一是off-the-shelf unsupervised similarity metrics现成的非监督相似性度量；一种是训练一个prompt retriever基于surface similarity来选取prompt。  
2. 使用类似对比学习的方法，通过概率来为样例打上positive和negative的标签。
3. 使用一个远小于Inference LM的proxy LM来选择example；或者直接用Inference LM来选择也可。
4. Efficient Prompt Retrieval（EPR，效率prompt检索）

## Background: Prompt Retrieval

1. 监督检索器为了knowledge-based queries, 依赖于surface similiarity

## Efficient Prompt Retriever

1. 直接使用gold truth $y$, 效果会有一定提升。

2. 训练的目标是一个similarity metric

3. ![image-20221226130653972](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221226130653972.png)

   对比训练目标函数，最小化负对数。
   ![image-20221226130823259](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221226130823259.png)

4. We focus on tasks that map utterances to meaning representations（将语义映射到意义表征的任务）。

## Experimental Result

![image-20221226154753585](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221226154753585.png)

这里的LM-ORACLE是EPR的理论最优值。

## BM25算法

https://zhuanlan.zhihu.com/p/420048609

BM25是目前信息索引领域最主流的计算query与文档相似度得分的算法。

BM 是Best Match最佳匹配的缩写，25指的是第25次算法迭代。

BM25的公式主要由几个部分组成：

1. query中每个单词的重要性（从IDF变形而来）
2. query中每个单词与文档之间的相关性（从TF变形而来，并考虑了文档的长度）
3. *query中每个单词与query的相关性（注意，这一部分计算公式只有当query很长时才会使用，所以在有些地方没有这部分内容，而有些地方有这部分内容）

![img](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/v2-17d45648e225a8818bad87a9b2c39e7f_r.jpg)



![image-20221227132132455](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20221227132132455.png)

