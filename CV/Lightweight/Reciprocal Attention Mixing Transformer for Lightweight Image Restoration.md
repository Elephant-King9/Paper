**Reciprocal Attention Mixing Transformer for Lightweight Image Restoration**. Haram Choi et.al. **arxiv**, **2023**, ([pdf](assets/pdfs/Reciprocal_Attention_Mixing_Transformer_for_Lightweight_Image__Restoration.pdf))([link](http://arxiv.org/abs/2305.11474v4)).

- **背景**

  - 

- **现有问题**

  - 当前图像复原方法存在两个主要问题
    - **参数过多**：尤其是Transformer架构，导致部署困难
    - **关注范围单一**：
      - 一些方法只处理**局部信息**，感受野有限；
      - 一些方法仅处理**全局依赖**，可能缺乏细节恢复能力；
      - 二者难以兼顾。

- **动机**

  - RAMiT旨在在轻量化的同时，**融合局部与全局信息建模能力**

- **贡献**

  - **提出D-RAMiT块**
  - **引入H-RAMi层**
  - **在五个轻量级图像复原任务上取得SOTA**

- **解决思路**

  - **D-RAMiT（Dimensional Reciprocal Attention Mixing Transformer）**

    - 同时进行**空间注意力**和**通道注意力**建模；
    - 每种注意力使用不同的多头数（multi-heads）并行进行；

  - **H-RAMi（Hierarchical Reciprocal Attention Mixing）**

    - 补偿由于下采样导致的像素级信息丢失；将来自不同层级（多尺度）的注意力结果进行融合

    

  - **MobileNetV2 模块整合**

    - 作者对 MobileNetV2 进行修改，将其高效卷积模块集成到 Transformer 中；
    - 进一步**减小计算成本**，增强模型推理速度。

- **具体解决办法**

