**CogView: Mastering Text-to-Image Generation via Transformers**

- **背景**

- **现有问题**

- **动机**

  - 提出了 CogView——一个拥有 40 亿参数、带有 VQ-VAE 分词器的 Transformer 模型，超越DALL·E

- **贡献**

  - **相比DALL·E,有四方面进步**

    -  **除了零样本生成，还可以微调做别的任务，比如风格学习、超分、生成图片描述、做图文排序等**

    -  **微调后的 CogView 可以实现自我重排，不需要像DALL·E,用 CLIP 模型来选结果**

    - **还提出了新指标Caption Loss用来更精准评估生成图像好不好**

    - > DALL-E 在生成多张图像后，需要额外用一个 **CLIP 模型** 来判断这些图像和文本描述的匹配程度，然后挑出最好的图像（因为 DALL-E 本身不会判断自己生成的图像和文本是否匹配得最好
      >
      > **微调后的 CogView** 自身学到了更强的 **图文对齐能力**，因此它可以 **在自己内部直接对生成的图像打分、排序**，选出和文本描述最匹配的图像，而不需要再依赖 CLIP 这种外部判别模型

    - **提出 PB-relaxation 和 Sandwich-LN，用来稳定大规模 Transformer 在复杂数据集上的训练,些技巧非常简单，能消除前向计算中的溢出,让模型不崩掉，并且能用更快地半精度训练，这些技巧也可以用到其他模型**

- **解决思路**

  - 由于数据差异性太大，大规模文本到图像的生成式预训练很不稳定，我们系统分析了原因，并提出精度瓶颈松弛（PB-relaxation）和夹心层归一化（Sandwich Layernorm）来解决。

- **具体解决方法**

  - VAE 或 VQ-VAE 框架通常固定先验分布（如标准高斯）来近似后验
    - CogView创新
      - 原本VQ-VAE使用简单的神经网络来将图像生成的潜空间序列映射到词典，而CogView在图像生成的潜空间前面添加文本，使用Transformer-Decoder来建立图像+文本对于词典的映射（VQ-VAE仅建立图像映射）
  - VAE 类模型通常端到端同时训练编码器、解码器和潜变量先验
    - **CogView 创新：**
      - VQ-VAE和CogView第一阶段是相同的，第二阶段VQ-VAE使用autoregressive而CogView使用Transformer-Decoder做自回归
  - 加大数据集数量，训练更具泛化性的模型
  - 自回归部分
    - 相比于DALL·E直接将文本和图像拼接一起计算损失权重,CogView序列中插入 [BASE], [BOI1], [EOI1] 等分隔符标记文本 / 图像 token 边界；保持文本 token 损失和图像 token 损失等权重分别计算，并通过大规模批量、稀疏注意力等手段优化效率
  - Precision Bottleneck Relaxation (PB-Relax)
    - 优化训练梯度，保证在反向传播时数值稳定可用，防止训练过程中LayerNorm和Attention梯度或者中间值溢出
  - Sandwich LayerNorm (Sandwich-LN)
    - 在残差连接和Attention前都加LayerNorm，DALL·E只在Attention前加，靠结构本身防止梯度/激活爆炸
  - 这两个方法不仅适用于 CogView，也能帮助任何大规模 Transformer 模型的训练。
  - 在微调部分针对不同任务使用不同的微调策略来实现提高不同下游任务的性能

- **实验**