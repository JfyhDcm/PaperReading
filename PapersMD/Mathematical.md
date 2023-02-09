# Mathematical Capabilities of ChatGPT

## Abstract

1. 形式数学（formal mathematics）有大量的形式证明的数据库（例如Lean Mathematical Library），而目前用来衡量语言模型的数据库一般只覆盖初等数学。
2. 提出了新的数据集GHOSTS：是第一个由相关数学家为语言模型构建的数据集；覆盖研究生水平的数学问题；提供语言模型的数学能力的整体概述
3. 与社交媒体上的结论相反，ChatGPT的高等数学能力远远低于一个研究生

## Intro

1. 下图为Twitter上语言模型的相关提及指数，其中横纵坐标为对数缩放的。

![image-20230205181656434](https://cdn.jsdelivr.net/gh/JfyhDcm/TC/img/image-20230205181656434.png)

2. 本文主要查看ChatGPT是否有以下的能力：完成有空白或缺失步骤的数学证明的能力；解决更注重深刻见解和原始解决方案的问题的能力，例如奥数竞赛的问题；以及调查文献和跨领域思考的能力(“我们还需要哪些定理来证明给定的定理?”)
3. 本文的三方面贡献：提供了数学应用方面的视角，什么类型和领域的数学ChatGPT可以解决；确定了ChatGPT的失效模式，以及其能力的短板，为以后发展LLM提供帮助；提供了一种可在LLM之间作比较的benchmark

## Related Work

对于ChatGPT，网上只有奇闻轶事的分享，对于数学性能的分析只有一个在高精度计算无理数的内容。

大型语言模型用不了formal mathematical dataset的原因还有其并没有自然语言版本，转化可能造成上下文错误。

## Datasets

构造了dataset集合，predicate全部由也只能由数学专家来打分。

## Results

1. 奥数风格的问题，ChatGPT表现得很糟糕
2. prompt长度基本不影响结果
3. step-by-step后，不太严重的错误变少了，更严重的错误保持不变，平均评级也基本不变
4. ChatGPT非常自信，不同于一般的GPT模型（如Codex）
5. 



