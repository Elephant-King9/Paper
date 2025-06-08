**Efficient Attention-Sharing Information Distillation Transformer forLightweight Single Image Super-Resolution**. Karam Park et.al. **arxiv**, **2025**, ([pdf](assets/pdfs/Efficient_Attention-Sharing_Information_Distillation_Transformer_for__Lightweight_Single_Image_Super-Resolution.pdf))([link](http://arxiv.org/abs/2501.15774v2)).

- **背景**
  - CNN 超分模型计算量大，尤其在深层网络中，显著限制了实用性。
  - 为此，研究者尝试了两类主要策略来提升效率和参数利用率：
    1. Weight Sharing（权重共享）：多个模块复用同一套参数，减少冗余。
    2. Feature Reuse（特征重用）：将早期特征多次利用（如 DenseNet 思想），避免重复计算。
  - 这些轻量化方法虽然有效率，但也限制了模型能力，导致：
    - 网络深度受限：因为权重共享后层数不能无限叠加，否则会过拟合或收敛困难。
    - 感受野受限：卷积天然局部，若不引入额外机制（如注意力），模型很难捕捉远距离依赖信息。
- **现有问题**
  - Transformer迫切需要轻量化、低参数量、高效率的工作量
- **动机**
  - 专门针对 Transformer-SR 的轻量化设计，解决Transformer在图像重建中的高计算负担问题。
- **解决思路**
  - **注意力共享(Attention-Sharing)**
    - 将多个Transformer模块之间的注意力权重共享，避免每层都单独重新计算attention，从而进一步减少计算量。
    - 跨Block共享注意力是一种创新的轻量策略。
  - **信息蒸馏结构(Information Distillation)**
    - 通过IDB模块实现
- **具体解决方法**
  - **IDB模块实现信息蒸馏**
    - **将输入特征按照重要性划分（例如按通道分割）**，保留一部分“精华”特征，另一部分继续送入后续模块精炼。
    - 特征被分为两个部分：
      - 一部分**精细特征**立即保留（用于最终拼接输出）。
      - 一部分**粗特征**继续深加工。
    - IDB由三个子模块组成
      - **LM**：卷积提取局部特征
        - PW(1x1卷积)用于通道压缩与融合，让特征更紧凑
        - SW(逐通道卷积)用更低的计算量提取空间结构
        - SE经两级通道注意力，增强重要通道，抑制冗余通道
        - ![image-20250523174327384](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Efficient Attention-Sharing Information Distillation Transformer for Lightweight Single Image Super-Resolution/image-20250523174327384.png)
      - **空间注意力(SAM)+通道注意力(CAM)**
        - 都采用窗口划分
        - 包含两个注意力阶段：中尺度注意力(**Meso-level attention**)+全局注意力(**Global-level attention**)
          - 中尺度注意力(**Meso-level attention**)
            - 仅在局部窗口进行注意力运算
          - 全局注意力(**Global-level attention**)
            - 考虑不同窗口之间的联系
            - ==也是局部的注意力，只不过相较于中尺度注意力窗口更大==
      - **通道划分与注意力参数共享**
        - 仅对空间注意力进行通道划分
        - 共享A矩阵，后续仅计算V矩阵
      - ![Snipaste_2025-05-23_18-16-19](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Efficient Attention-Sharing Information Distillation Transformer for Lightweight Single Image Super-Resolution/Snipaste_2025-05-23_18-16-19.jpg)
    - ![image-20250523173850495](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Efficient Attention-Sharing Information Distillation Transformer for Lightweight Single Image Super-Resolution/image-20250523173850495.png)











![image-20250523172912300](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Efficient Attention-Sharing Information Distillation Transformer for Lightweight Single Image Super-Resolution/image-20250523172912300.png)

- 上采样模块







==线性结构，使用了通道注意力+窗口注意力，并使用通道划分蒸馏(区别对待不同重要性的同奥)和Attention权重共享来解决Transformer轻量化的问题==