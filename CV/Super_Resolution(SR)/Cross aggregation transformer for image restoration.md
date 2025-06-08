**Cross Aggregation Transformer for Image Restoration**. Zheng Chen et.al. **arxiv**, **2022**, ([pdf](assets/pdfs/Cross_Aggregation_Transformer_for_Image_Restoration.pdf))([link](http://arxiv.org/abs/2211.13654v2)).

- **背景**
  - 虽然Transformer在视觉领域展现出强大长距离建模能力，但其高昂的计算复杂度以及现有局部窗口/通道注意力方法的缺陷（跨窗口交互弱、空间信息丢失）限制了其在高分辨率图像修复中的应用与效果。
- **现有问题**
  - 全局注意力机制计算复杂度很高。很多方法采用了 局部方形窗口（如 Swin Transformer） 之间彼此独立，缺乏直接交互。导致模型难以有效建模 长距离像素之间的依赖关系。
- **动机**
  - 在不牺牲效率的前提下，实现跨窗口的全局信息交互
- **解决思路**
  - **Rwin-SA(矩形窗口注意力)**
    - Rwin-SA不同于传统方形窗口，而是采用矩形窗口（高≠宽），这样可以灵活调整注意力区域的形状。
  - **Axial-Shift(轴向偏移)**
    - 原理类似 Swin Transformer 的“Shifted Window”，但方向更具针对性（横/纵轴）。
  - **LCM**
    - 在自注意力中直接对V引入局部卷积
  - **在SR任务上使用RIR结构，在IR任务上使用Unet结构**
- **具体解决方法**
  - **Rwin-SA(矩形窗口注意力)+Axial-Shift(轴向偏移)**
    - Rwin-SA(矩形窗口注意力)使用水平长条和竖直长条窗口注意力，在不增加计算复杂度的前提下，显著扩展了注意力范围，同时增强了水平与垂直特征的融合。使注意力机制能自然地跨多个方形区域建立连接，打破窗口边界限制.
    - Axial-Shift(轴向偏移)提升不同窗口之间的特征融合能力。这种设计可以增加跨窗口交互，获得更大的感受野。轴向shift更加明确地增强了水平方向或垂直方向窗口的交互。同时间接促进水平和垂直窗口的交叉交互。
    - ![image-20250516113721516](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Cross aggregation transformer for image restoration/image-20250516113721516.png)
  - **LCM**
    - 左边是Rwin-SA，对 Q, K, V 进行自注意力。
    - 右边是LCM，直接对 V 进行 3×3 深度卷积。
    - 二者并行执行，最后加和后经过Projection层。
    - 实现了全局动态建模（Attention）+局部静态建模（Conv）的融合，提升了CAT对局部细节的感知能力，同时保持高效的全局信息聚合。
    - ![image-20250516114013869](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Cross aggregation transformer for image restoration/image-20250516114013869.png)

==使用长方形的窗口注意力+偏移来解决现有Transformer的问题，同时在Attention时并行加入卷积来提高学习能力，在IR任务上使用Unet结构，在SR任务上使用RIR结构==

- **上采样部分**

  - ```mermaid
    flowchart LR
    	subgraph conv_before_upsample
    		direction LR
    		A[B,96,16,16]-->|conv（96,64）|B[B,64,16,16]-->|RELU|C[B,64,16,16]
    	end
    	C-->2x[2x]-->D
    	C-->3x[3x]-->G
    	C-->4x[4x]-->J
    	subgraph Upsample_RCAN
    		direction LR
    		D[B,64,16,16]-->|conv（64,4*64）|E[B,4*64,16,16]-->|PixelShuffle（2）|F[B,64,32,32]
    	end
    	subgraph Upsample_RCAN
    		direction LR
    		G[B,64,16,16]-->|conv（64,9*64）|H[B,9*64,16,16]-->|PixelShuffle（3）|I[B,64,48,48]
    	end
    	subgraph Upsample_RCAN
    		direction LR
    		J[B,64,16,16]-->|conv（64,4*64）|K[B,4*64,16,16]-->|PixelShuffle（2）|L[B,64,32,32]-->|循环|J
    		F-->|conv（64,1）|M[B,1,H,W]
        I-->|conv（64,1）|M[B,1,H,W]
        L-->|conv（64,1）|M[B,1,H,W]
    	end
    ```

