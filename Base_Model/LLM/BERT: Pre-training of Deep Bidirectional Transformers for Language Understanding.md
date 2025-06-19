**BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding**

- **背景**
- **现有问题**
  - 认为GPT-1使用Decoder单向编码会存在全局语义的盲区
- **动机**
  - ELMo RNN+双向，GPT Transformer+单向，融合BERT Transformer+双向

- **贡献**
  - **展示了双向预训练对语言表示的重要性**
  - **一个统一模型+微调可以适应不同任务,且效果很好**
  - **在11项自然语言处理任务上实现SOTA**
- **解决思路**
  - **预训练+微调**
  - **双向学习**
  - **输入两个句子，预训练两个任务**
    - [MASK]填词(完形填空)
    - 判断句子的是否相邻([CLS])

- **具体解决办法**
- **实验**
  - **数据集**
    - **预训练**
      - **BooksCorpus(800M words,GPT-1使用)**
      - **English Wikipedia(2500M words)**
  - **模型参数**
    - **BERT-base**
      - **Transformer encoder层数:12层**
      - **特征维度:768维**
      - **多头注意力头数:12**
      - **参数量: 110M**
    - **BERT-large**
      - **Transformer encoder层数:24层**
      - **特征维度:1024维**
      - **多头注意力头数:16**
      - **参数量:340M**
    - **微调**
      - **batch_size:32**


