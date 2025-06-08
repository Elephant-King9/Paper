**Multi-scale Attention Network for Single Image Super-Resolution**. Yan Wang et.al. **arxiv**, **2022**, ([pdf](assets/pdfs/Multi-scale_Attention_Network_for_Single_Image_Super-Resolution.pdf))([link](http://arxiv.org/abs/2209.14145v3)).

- **背景**

  - 卷积网络（ConvNet）如果采用 **更大的感受野**（例如大卷积核、大步长卷积），在高层任务中（如分类、检测）也能和Transformer竞争,这打破了“Transformer天然比CNN强”的刻板印象。

  -  Transformer逐步取代ConvNet成主流 ConvNet的“反击”：ConvNeXt和VAN尝试改进VAN以追赶Transformer

- **现有问题**

  - VAN的核心机制LKA的问题
  - 膨胀卷积引入块状伪影
    - 固定感受野不灵活

- **动机**

  - 作者想要将“Transformer并非天然比CNN强”**迁移到图像超分任务中**，探索CNN的上限。
  - 尝试改进VAN以追赶Transformer，改进VAN的LKA存在的膨胀卷积引入块状伪影与固定感受野不灵活的问题
  
- **解决思路**
  - **RIR网络结构**
  - **多尺度大核注意力(Multi-scale Large Kernel Attention ,MLKA)**
    - 融合大卷积核、多尺度、门控机制；
    - 同时建模局部与远程依赖，提升表示能力。

    - **MLKA** 是MAN中的主干注意力模块**采用 Transformer 的 MetaFormer 结构**

    - **多尺度建模（multi-scale）**
      - 通过不同大小的卷积核（小、中、大），分别关注图像的不同细节（局部/中远距离/全局结构）；
  
    - **门控机制（gate scheme）**
      - 引入**门控机制**（如Sigmoid权重选择），以动态调节不同尺度的注意力权重
      - 最终输出融合多个尺度的信息，并避免**特征“拼接边界”引起的块状伪影（blocking artifacts）**。
  - 简化MLP替代结构**(Gated Spatial Attention Unit ,GSAU)**
  
    - 移除传统注意力中多余的线性映射层（简化结构）；
    - 使用 **门控 + 空间注意力** 更好地选择“哪些区域更重要”；
    - 更轻量、更高效。
  
- **具体解决方法**
  - **MLKA+GSAU**
    - 传统如 RCAN 的结构是：Conv → 激活 → Conv → Attention
    - 本文采用 MetaFormer 框架（Transformer常用）：Norm → Token Mixer（注意力）→ Norm → FFN（简化为GSAU）
    - 这种设计对规范化、更深层建模和训练稳定性更友好。
  - ![image-20250518132559962](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Multi-scale Attention Network for Single Image Super-Resolution/image-20250518132559962.png)





![image-20250518132439554](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Multi-scale Attention Network for Single Image Super-Resolution/image-20250518132439554.png)

==RIR架构，CNN网络，旨在追赶CNN与Transformer的差距，对VAN进行改进，引入多尺度大核卷积和门控机制，同时采取类似于Transformer的架构设计，降低了CNN在SR工作上与Transformer的差距，但是在SR的性能上仍小于等于SwinIR( ×2/×3 任务基本持平，x4小于)==

- **上采样部分**

  - ```mermaid
    flowchart LR
    	2x[2x]-->D
    	3x[3x]-->D
    	4x[4x]-->D
    subgraph Upsample_RCAN
    		direction LR
    		D[B,180,16,16]-->|conv（180,1*scale^2）|E[B,scale^2*1,16,16]-->|PixelShuffle（scale）|F[B,1,32,32]
    	end
    ```
    
  - 