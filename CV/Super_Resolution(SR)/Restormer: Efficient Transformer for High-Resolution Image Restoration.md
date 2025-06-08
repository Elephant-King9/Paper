**Restormer: Efficient Transformer for High-Resolution Image Restoration**. Syed Waqas Zamir et.al. **arxiv**, **2021**, ([pdf](assets/pdfs/Restormer:_Efficient_Transformer_for_High-Resolution_Image_Restoration.pdf))([link](http://arxiv.org/abs/2111.09881v2)).

- **背景**
  - CNN 在图像恢复（如去噪、去模糊、去雨等）任务中表现良好因此，CNN 被广泛应用于图像修复相关任务。但是CNN的**感受野有限**（难以捕获长距离依赖）与**卷积核权重在推理时固定**，无法根据输入图像内容自适应调整。但Transformer的缺点是**计算复杂度与输入图像分辨率呈平方级增长**，这使得它难以应用于高分辨率图像修复任务。目前仅有少量工作尝试将Transformer适配到图像修复任务中。
  
- **现有问题**
  
  - 现有CNN在图像修复任务中面临感受野受限与无法自适应的问题，而Transformer的自注意力机制虽能缓解这些缺陷，计算复杂度高。
  - 已有工作通过局部窗口或patch分割方式减少复杂度（仅在每个像素周围的 **8x8小窗口** 内计算SA（局部注意力）或将图像划分为 **48x48的独立patch**，对每个patch独立计算SA。），但也削弱了自注意力捕捉长距离依赖的能力。
  
- **动机**
  
  - 设计一个Transformer网络，能在保持较低计算量的同时仍能捕获图像中的长距离像素依赖，解决经典Transformer算力开销过大的问题。
  
- **解决思路**
  
  - **注意力部分提出MDTA**
    - 一种改进的多头注意力机制，将注意力计算从“空间域”转移到“通道域”
    
  - **对于FFN部分提出GDFN**
    - 用“门控机制”替代原FFN的第一层线性映射，学会选择性放行有用特征，抑制无用特征.
  
  - **渐进式训练策略**
    - 初期用小patch进行训练，确保快速收敛。后期逐步扩大patch尺寸，增强模型的全局感知能力。这种策略有效帮助Restormer适应大分辨率图像的上下文学习，带来显著性能提升。
  
- **具体解决方法**

  - **MDTA**
    - 将矩阵进行转置，在通道的维度上计算注意力，更加适合高分辨率图像
    - ![image-20250515194537715](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Restormer: Efficient Transformer for High-Resolution Image Restoration/image-20250515194537715.png)
  - **GDFN**
    - 引入了3x3卷积，添加了对周围像素的学习
    - 使用两个分支做线性变换，一路加非线性，一路保留原始信息（门控机制）
    - 初始FFN
    - ![image-20250515195018959](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Restormer: Efficient Transformer for High-Resolution Image Restoration/image-20250515195018959.png)
    - 改进后的GDFN
    - ![image-20250515194708953](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Restormer: Efficient Transformer for High-Resolution Image Restoration/image-20250515194708953.png)
  - **渐进式训练**
    - 输入图像的尺寸不变，前期将图像裁剪为小块(32x32)进行学习，随着训练的进行会逐渐变大，直到不进行裁剪

==提出了基于通道的注意力，并定义了新型的前馈网络，同时在训练的过程中使用渐进学习，来解决现有Transformer无法处理高分辨率图像的问题==