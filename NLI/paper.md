## [Bilateral Multi-Perspective Matching for Natural Language Sentences (2017)](https://arxiv.org/pdf/1702.03814.pdf)
---
### 模型概要
#### **字词表示层**：
使用Glove作为embedding

#### **内容表示层**：
一层BiLSTM

#### **匹配层**：
1. 首先定义函数$f=cos(W * v1, W * v2)$其中$W$的大小为$l*dim$
2. 接下来以$P->Q$的匹配(即每个$h_i^P$匹配所有$h_j^Q$)列举四种匹配方法
   1. **全匹配**，对于所有$h_j^Q$只拿最后一项与$h_i^P$进入函数$f$
   2. **池化层匹配**, 对于所有$h_j^Q$都与$h_i^P$进入函数$f$最后进一层MaxPooling层
   3. **注意力匹配**，对于所有$h_j^Q$都与$h_i^P$求余弦值，将其作为$Query$，将$h_j^Q$作为$Key$,最后将得到的所有attension值求平均值与$h_i^P$进入函数$f$
   4. **Max注意力匹配**，前几步与step3类似，只是最后不是求平均而是将最大值与$h_i^P$进入函数$f$
3. 最后将这四种匹配法$concat$作为该层的输出

#### **聚合层**
将匹配层的四种匹配法则丢进BiLSTM进行聚合

最后一个time_step作为该层的输出

#### **预测层**
两层FNN+softmax

### 模型参数
* 300-dim 840B Glove (no grad)
* 100-dim BiLSTM
* 20 fix-length
* 0.1 dropout
* 0.001 learning-rate
* Cross-Entropy as LossFunction

## [Neural Natural Language Inference Models Enhanced with External Knowledge](https://arxiv.org/pdf/1711.04289.pdf)

TODO

## [Multi-Task Deep Neural Networks for Natural Language Understanding](https://arxiv.org/pdf/1901.11504.pdf)

TODO

## [Semantics-aware BERT for Language Understanding](https://arxiv.org/pdf/1909.02209.pdf)

TODOs