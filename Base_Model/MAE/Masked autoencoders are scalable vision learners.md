**Masked Autoencoders Are Scalable Vision Learners**. Kaiming He et.al. **arxiv**, **2021**, ([pdf](assets/pdfs/Masked_Autoencoders_Are_Scalable_Vision_Learners.pdf))([link](http://arxiv.org/abs/2111.06377v3)).

- **背景**
  - NLP本身语义非常密集，一句话中的每一个词都有独特且不可替代的语义价值，而图像具有强空间冗余性，例如一个天空区域的多个 patch 看起来几乎一样，遮掉其中某一 patch，只需周围 patch 就能“无脑”恢复，无需高层语义理解
- **现有问题**
  - 分析为什么NLP存在BERT而视觉方面没有这种工作？
    - CNN不适合直接使用MASK，而CV在ViT后才开始将图像分patch进行处理
    - NLP本身语义非常密集，一句话中的每一个词都有独特且不可替代的语义价值，而图像具有强空间冗余性，例如一个天空区域的多个 patch 看起来几乎一样，遮掉其中某一 patch，只需周围 patch 就能“无脑”恢复，无需高层语义理解
    - CV的decoder更难设计，如果decoder太简单，则只会恢复局部纹理
      - CV中的自编码器和NLP中的有本质差异
        - CV中decoder是为了重建像素级别的图像内容，输出是每个像素的RGB值与局部纹理边缘结构，都是低层次的视觉特征，而不是什么物体或什么场景，模型肯呢个只学会了图像平滑，纹理不全
          - **重建像素≠学习语义信息**
        - NLP中要预测的是单词
          - 单词本身就有强语义，要预测对就要理解上下文
- **动机**
  - 提出了一种自监督视觉学习方法，不需要人工标签，通过遮挡部分图像再回复原图，来自监督训练模型
- **解决思路**
  - **不对称编码器-解码器结构**
    - **不对称**
      - 传统的自编码器的encoder和decoder通常对称，而MAE打破了这种设计
    - **编码器**
      - 只处理可见部分的patch，避免无效计算
    - **解码器**
      - 输入编码表示+mask token来预测整图
  - ![image-20250608211123094](/Users/sitianyi/Paper/Base_Model/MAE/assets/pics/Masked autoencoders are scalable vision learners/image-20250608211123094.png)
  - **高遮挡率设计**
    - 遮挡75%的图像不仅可以训练成功，反而促进了更好的表征学习
    - 且训练速度更快（encoder只处理少量patch）



- **具体解决方法**

  - **MASK部分**

    - 使用均匀分布不放回采样，意味着不会重复选择同一个patch
    - 高遮挡率能破坏附近patch推理的可能性，强迫模型理解全局结构和语义，而非考局部补全

  - **Encoder部分**

    ```mermaid
    flowchart LR
      subgraph encoder
      	direction LR
        未被遮挡的25%patch-->|线性变化|向量
        位置编码-->|add|向量
        向量--> ViT
      end
      ViT-->encoder学习到的25%patch
    ```
    
    - 被遮挡的75%完全不参与encoder，不同于BERT使用[MASK]占位，而是直接删掉被遮挡部分，计算量大减
    
  - **Decoder部分**
  
  - ```mermaid
    flowchart LR
    	encoder学习到的25%patch-->添加位置编码
    	被遮挡的75%mask_token-->添加位置编码
      subgraph encoder
      	direction LR
      	添加位置编码-->ViT
      end
    ```
  
    - 实验中使用的decoder计算量仅为encoder的10%，且仅在预训练阶段使用
  
  - **损失部分**
  
    - 仅需要计算被遮挡的75%的损失
  
    - 使用均方误差（MSE）
  

