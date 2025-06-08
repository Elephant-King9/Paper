**Swift Parameter-free Attention Network for Efficient Super-Resolution**. Cheng Wan et.al. **arxiv**, **2023**, ([pdf](assets/pdfs/Swift_Parameter-free_Attention_Network_for_Efficient_Super-Resolution.pdf))([link](http://arxiv.org/abs/2311.12770v3)).

- **背景**
  - 
  
- **现有问题**

  - **已有的一些方法通过减少计算量（FLOPs）或参数量提升效率**，但问题是降低 FLOPs/参数 ≠ 推理更快：实际推理速度不仅受 FLOPs 影响，还和内存访问、框架实现有关。

    

- **动机**
  - 创建一个快速的、无参数注意力机制、平衡参数量、推理速度和图像质量三者

- **解决思路**
  - **无参数注意力机制（纯CNN）**
    - **对称激活函数（如 ReLU²）**
      - 不引入额外可学习参数，而是将提取到的特征送入一个**以原点对称的激活函数**（如 ReLU²），直接用于计算注意力图。
      - **残差连接**：避免因为激活函数的稀疏性而导致信息损失，帮助保持模型稳定性。

- **具体解决方法**

![image-20250603205128613](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Swift Parameter-free Attention Network for Efficient Super-Resolution/image-20250603205128613.png)

==设计了一个纯CNN网络，用CNN+非线性来实现SR网络，用非线性的结果与CNN结果相乘来指导特征图更新，来实现用少量参数媲美Attention的效果==