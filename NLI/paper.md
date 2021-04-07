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
---
## [Neural Natural Language Inference Models Enhanced with External Knowledge](https://arxiv.org/pdf/1711.04289.pdf)
---

### 模型概要
该模型只是在ESIM模型的基础上定义了一个relation features $r_{ij}$
#### **Encoding部分**
pre-train+BiLSTM
#### **匹配部分**
求出两句话的相似矩阵$e_{ij}$,为了给相似矩阵引入知识，直接将$e_{ij}$与$F(r_{ij})$求SUM。
* paper中提到$F$可以是简单的$Linear$,也可以是一个激活层、或是一个参数$\lambda$。效果都差不太多
#### **推理表示层**
---

## [Semantic Sentence Matching with Densely-connectedRecurrent and Co-attentive Information](https://arxiv.org/pdf/1805.11360.pdf)
---
### 模型概要
该模型通过embedding层后经过多层稠密连接的$(RNN+Co-Attention+Bottleneck   -component)* N$,最后过一层prediction层+FC(ReLU激活)

#### **Embedding**
* 常用的预训练模型Glove、Word2vec
#### **Densely-connected RNN**
* 每层的RNN结构作者使用了BiLSTM，为了防止神经网络过深导致的梯度消失，作者采用级联方式即每层的输入与输出结合(concat)作用于下一层的输入
  
  $$h_t^l=H_l(x_t^l,h_{t-1}^l)$$
  $$x_t^l=[h_t^{l-1};x_t^{{l-1}}]$$
#### **Densely-connected co-attentive**
改成方式为常见NLI匹配层的方式，但是由于该网络层为多层结构，为了防止梯度消失，作者也把co-attentive的结果concat到下一层的输入令$a$为co-attentive的结果，则下层的输入为$x_t^l = [h_t^{l-1};a_t^{l-1};x_t^{l-1}]$

#### **Bottleneck component**
由于每层的输出都会级联到下层的输入，这就必然导致深层网络的维度暴炸，因此引入AE(Autoenoder)在保留原始信息的同时减少feature数量

#### **prediction layer**
* 将稠密连接网络的输出中的词长这一维进行max-pooling(即将batch_size * len * dim -> batch_size * dim)
* 拼接两句话的结果$v=[p;q;p+q;p-q;|p-q|]$
* 将拼接结果进入全连接层(使用ReLU作为激活函数)
---
## [Explicit Contextual Semantics for Text Comprehension](https://arxiv.org/pdf/1809.02794.pdf)
---
### 模型概要
* 整体模型以ESIM为基准把embedding层改成word embedding pre-train与SRL embedding拼接以得到引入语义信息的作用

#### **SRL**
* 作者使用一个简单的BiLSTM模型在OntoNotes v5.0数据集上训练得到SRL模型

#### **NLI**
* 作者将训练好的SRL用于embedding的拼接，将原本词的embedding拼接上SRL模型得到的语义embedding作为整个模型的embedding


---
## [Multi-Task Deep Neural Networks for Natural Language Understanding](https://arxiv.org/pdf/1901.11504.pdf)
---
TODO

---
## [Semantics-aware BERT for Language Understanding](https://arxiv.org/pdf/1909.02209.pdf)
---
TODO

---