**SRConvNet: A transformer-style ConvNet for lightweight image super-resolution**

- **背景**

  - 

- **现有问题**

- **动机**

  - 深入分析了 ConvNet 与 Transformer 在图像超分中的关键差异，并提出了一种融合二者优势的模型：**SRConvNet**，以实现轻量化与建模能力的统一。
  - 本质采用卷积 + 频域建模机制来替代 MHSA

- **贡献**

  - **提出SRConvNet模型**
  - **设计FMA**
  - **设计DML**

- **解决思路**
- **ACB**
    - **FMA**
    - FMA 是一个模拟 MHSA 功能但更高效的注意力机制，核心特点：
      - **在频域与空间域**同时进行调制与特征聚合；
      - **保留 多头注意力(MHSA) 的全局建模能力**，同时显著减少计算量；
      - 能够同时建模 **长期（全局）与短期（局部）依赖**
      - 将输入特征划分为多个**非重叠局部区域**（patch/grid）
      - 对每个 patch 进行 **傅里叶变换（FFT）→ 频域调制 → 逆变换（iFFT）**
    - **DML**
    - 动态卷积
  
    - 使用 **多尺度深度可分离卷积（depthwise convolution）**，提升多尺度建模能力；
  
    - 通过 **通道切分与打乱（splitting & shuffling）** 增强通道间信息交互；
  
    - **Mixed-Scale Dynamic Convolution（多尺度动态卷积）**
        - 不同尺度的卷积核（如 3×3、5×5）并行建模，提取多尺度上下文信息
      - 卷积权重是 **动态生成的**，即根据输入内容自适应调整（提升灵活性）
      - **Channel Splitting（通道划分）**
      - 将通道分组处理，每组使用不同的卷积策略，提升表达多样性
      - **Channel Shuffling（通道打乱）**
        - 将各通道信息打散后重新组合，**加强特征混合与跨通道交互**（类似 ShuffleNet）

- **具体解决办法**