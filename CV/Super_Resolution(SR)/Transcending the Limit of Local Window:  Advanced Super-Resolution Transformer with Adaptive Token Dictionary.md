**(SR)Transcending the Limit of Local Window: Advanced Super-Resolution Transformer with Adaptive Token Dictionary**. Leheng Zhang et.al. **arxiv**, **2024**, ([pdf](assets/pdfs/Transcending_the_Limit_of_Local_Window:_Advanced_Super-Resolution__Transformer_with_Adaptive_Token_Dictionary.pdf))([link](http://arxiv.org/abs/2401.08209v2)).

- **背景**

  - 早期超分字典学习是经典方法，这类方法通过从训练图像中学习一个字典，每个低分辨率图像块可以在该字典中找到若干相似原型（atoms），这类方法通过从训练图像中学习一个字典，每个低分辨率图像块可以在该字典中找到若干相似原型（atoms）
- **现有问题**
- **动机**

  - 借鉴传统超分方法中的字典学习思想，平衡窗口与计算量之间的关系
- **解决思路**

  - **Token字典(Token Dictionary)**
    - 全局共享
  - **利用 Token Dictionary 实现语义分组的 Category-Based Self-Attention**
    - 将所有 image token 按照其最相似的 dictionary token 分组
  - **组合两种注意力机制以建模长距离依赖并提升性能**
  - **TDCA(Token Dictionary Cross-Attention)**
    - 引入一个额外的、全局共享的 **token dictionary D**，作为外部结构先验来源
- **具体解决办法**
  - **TDCA**
    - Q是根据输入特征得到
    - KV是从字典D中得到
    - Q@K使用预选相似度计算而不是点乘，有利于保证字典token被公平考虑
  - **AC-MSA**
    - 利用 TDCA 产生的attention map A，每个 token 对应于字典中哪个原型 token（先验结构）最相似；
    - 根据最大注意力值所在的字典 token 索引，将所有 token 分组为 M 类（如：边缘类、纹理类等）