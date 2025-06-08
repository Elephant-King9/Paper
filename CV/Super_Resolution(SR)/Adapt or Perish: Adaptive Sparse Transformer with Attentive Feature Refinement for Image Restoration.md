**Adapt or Perish: Adaptive Sparse Transformer with Attentive Feature Refinement for Image Restoration**

- **背景**
  - CNN方法虽取得进展，但**卷积的感受野有限，难以捕捉长距离依赖**，因此在复杂场景下存在瓶颈。Transformer通过**自注意力机制**解决了CNN的感受野限制，能够建模全局关系。但其**计算复杂度高**，尤其在高分辨率图像上不够高效。
  
- **现有问题**
  - 传统的窗口Attention会和图片中的每一个部分进行计算，但是大部分信息和本像素无关，就造成了需要计算冗余的信息，大量浪费时间在建立与无关信息的联系上
  
  - ![image-20250516190750247](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Adapt or Perish: Adaptive Sparse Transformer with Attentive Feature Refinement for Image Restoration/image-20250516190750247.png)
  
- **动机**

  - 作者希望探索一个新的方案：在保证减少噪声特征的同时，尽可能保留有用特征，避免现有稀疏注意力方法的局限。
  
- **解决思路**

  - **Unet+窗口注意力**
  - **适应性稀疏自注意力(ASSA)**
    - **SSA（稀疏分支）**
      - 关注重要交互，剔除噪声和无关token。
    - **DSA（密集分支）**：
      - 留完整信息流，防止信息丢失。
    - 两个分支的输出通过自适应加权融合，更聚焦在有用区域
  - **特征精炼前馈网络(FRFN)**
  - 改进FFN，在通道维度压缩冗余，提升特征紧凑度。过滤掉不必要的通道信息。
  
  - ![image-20250516190945308](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Adapt or Perish: Adaptive Sparse Transformer with Attentive Feature Refinement for Image Restoration/image-20250516190945308.png)
  
- **具体解决方法**
  - **ASSA**
    - **SSA(稀疏自注意力)**
      
      - 使用**平方ReLU**过滤掉低匹配分数（Query-Key相似度低）的交互
      
      - > 为什么平方ReLU可以过滤无关部分？
        >
        > - $$ReLU(x) = max(0, x)$$
        >
        > - 所有小于0的值会被强制置0。只有正值会被保留。Attention Score是负数时，ReLU会直接过滤掉这些低相关性的query-key对，这样很多交互被“硬性剪掉”，自然形成稀疏矩阵
        >
        > - 平方ReLU进一步强化稀疏性（负数仍然为0，正数被平方后更极端），使得高匹配得分被放大，低匹配得分变得更不重要。
      
    - **DSA(密集注意力)**
    
      - 引入传统的Softmax-based DSA，保证信息流充足，补偿SSA过稀疏导致的信息丢失
    
      - > 为什么Softmax可以保留全局信息?
        >
        > - $$Softmax(x) = exp(x) / Σexp(x)$$
        >
        > - 无论输入多少，输出都是正数。每个query都会关注所有key，只是注意力分布不同
      
    - ![image-20250516200715638](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Adapt or Perish: Adaptive Sparse Transformer with Attentive Feature Refinement for Image Restoration/image-20250516200715638.png)
    
  - **FRFN**

    - 尽管ASSA有效地在空间维度上（位置维度）减少了冗余信息。但在通道维度（feature maps的C维）仍然存在大量冗余信息。
    
    - >  PConv:只对部分通道执行卷积，减少计算量，同时引入局部感知能力。
    
    - ![image-20250516201840803](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Adapt or Perish: Adaptive Sparse Transformer with Attentive Feature Refinement for Image Restoration/image-20250516201840803.png)



==提出了适应性稀疏自注意力和特征精炼前馈网络FNN，分别在空间和通道维度降低了信息冗余，解决了目前窗口注意力存在信息冗余的问题==
