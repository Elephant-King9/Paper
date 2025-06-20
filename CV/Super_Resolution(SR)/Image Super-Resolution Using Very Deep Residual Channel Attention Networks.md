**Image Super-Resolution Using Very Deep Residual Channel Attention Networks**. Yulun Zhang et.al. **arxiv**, **2018**, ([pdf](assets/pdfs/Image_Super-Resolution_Using_Very_Deep_Residual_Channel_Attention
__Networks.pdf))([link](http://arxiv.org/abs/1807.02758v2)).

- **背景**

  - 基于深度卷积神经网络（CNN）的超分方法在性能上远超传统方法（如基于插值、稀疏表示等算法），成为主流。
  - 更深的网络在超分辨率的工作上更强。网络的深度（表示能力）在图像超分任务中非常重要，越深的网络越能学到丰富的特征表示。然而，仅仅堆叠更多残差块来增加深度，并不能无限提升性能。一方面训练变难，另一方面容易过拟合或梯度消失。
  
- **现有问题**
  
  - 越深的网络理论上能捕获越复杂的特征，有助于重建更精细的图像。但是过深的网络训练过程中容易出现梯度消失、过拟合等问题
  - 图像中一些比较“平滑”的区域占主导，而CNN没有能力自动“偏重”高频（细节）信息，从而难以有效还原图像细节
  - 现有大多数 CNN 方法对于特征图中的不同通道，一视同仁，没有区分哪些通道更有价值（比如哪些包含高频信息）。这会导致模型在处理低频与高频信息时缺乏灵活性，不能有针对性地提取有用特征。对所有通道平均对待，不加选择。这样其实浪费了对低频通道的计算资源，同时也没有强化对高频特征的学习能力。
  
- **动机**
  
  - 创建了非常深且能训练的神经网络，不易梯度消失或梯度爆炸的残差通道注意力网络
  
  - 使神经网络专注于高频信息学习，尽量忽略已经在低分辨率图像中的低频信息的学习
  
- **解决思路**
  
  - **RIR(残差中的残差)结构**
    - 可以使主干网络专注于高频信息的学习，并可以在非常深的情况下也可以训练
  - **通道注意力机制**
    - 可以区分那些通道更有价值，将高频信息通道与低频信息通道进行区分
  - **上采样部分**
    - 后上采样策略，在网络最后阶段再进行上采样，相比“先上采样”的超分方法（如 DRRN 和 MemNet），在计算复杂度和性能上都更高效。
  
- **具体解决方法**
  - **RIR结构**
    
    - 残差连接为什么能“绕过”低频信息？
    
      - 图像中的低频信息（如平滑区域、轮廓、颜色块）本身在低分辨率图像中就已存在。这些信息相对简单、易恢复，且在特征提取过程中会频繁出现（是“主导成分”）。然而超分辨率真正需要补充的是**高频细节信息**（如边缘、纹理、小结构）。skip connection 本质是将输入特征 **“直接绕过”部分计算单元**，传递给后续模块。它**不做额外特征变换**，相当于**信息的无损旁路**。因此，跳跃连接更倾向于**原样保留**那些易于建模、变化不大的成分（比如低频信息）。
      - **低频信息**：在网络中“直接走捷径”快速传递，从而避免在大量卷积中被“重新学习”或“误调整”。
      - **高频信息**：无法通过skip connection“绕过去”，只能通过残差路径不断被网络学习、增强。
    
    
    ![image-20250515165905894](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Image Super-Resolution Using Very Deep Residual Channel Attention Networks/image-20250515165905894.png)
    
    
    
  - **通道注意力机制**
  
    - 先通过全局平均池化将一整个通道转化为一个评分（H~GP~），通过加入非线性的W~D~与W~U~的通道变化，相当于一个组合的过程，可以让神经网络自动去学习哪些通道组合意味着有用的高频信息，哪些组合是冗余的，最后通过$$f$$（Sigmoid）来对各个通道进行评分，然后通过主元素相乘来改变每个通道的权重来实现通道重要性再分配。
    - ![image-20250515165951304](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Image Super-Resolution Using Very Deep Residual Channel Attention Networks/image-20250515165951304.png)

==针对超分辨率深度卷积网络不好训练以及现有模型未能区分高频信息和低频信息的问题，分别提出RIR残差结构和通道注意力进行解决，上采样部分使用低分辨率域处理 + 后期上采样 + 简洁重建来重建==

- 上采样部分

  - ```python
    n_feats = 64
    ```
  
  
  - > PixelShuffle(upscale_factor=r) 会将 shape 为 (B, C×r², H, W) 的张量，变换为 (B, C, H×r, W×r)。
  
  - ```mermaid
    flowchart LR
    2x[2x]-->|B,C,H,W|A
    3x[3x]-->|B,C,H,W|D
    4x[4x]-->|B,C,H,W|G
    subgraph Upsample
    		direction LR
    			A[B,64,16,16]-->|conv（64,4*64）|B[B,4*64,16,16]-->|PixelShuffle（2）|C[B,64,32,32]
    			D[B,64,16,16]-->|conv（64,9*64）|E[B,9*64,16,16]-->|PixelShuffle（3）|F[B,64,48,48]
    			G[B,64,16,16]-->|conv（64,4*64）|H[B,4*64,16,16]-->|PixelShuffle（2）|I[B,64,32,32]-->|循环|G
          C-->|conv（64,1）|M[B,1,H,W]
          F-->|conv（64,1）|M[B,1,H,W]
          I-->|conv（64,1）|M[B,1,H,W]
    end
    ```
