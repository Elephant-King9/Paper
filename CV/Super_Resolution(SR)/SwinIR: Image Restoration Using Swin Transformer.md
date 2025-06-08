**SwinIR: Image Restoration Using Swin Transformer**. Jingyun Liang et.al. **arxiv**, **2021**, ([pdf](assets/pdfs/SwinIR:_Image_Restoration_Using_Swin_Transformer.pdf))([link](http://arxiv.org/abs/2108.10257v1)).

- **背景**
  - 当前最先进的（SOTA）图像复原方法主要基于 **CNN（卷积神经网络）**，而 **Transformer** 虽然在高级视觉任务（如分类、检测）中表现优异，但在图像复原领域的研究较少。
- **现有问题**
  
  - 现有使用Transformer进行图像恢复大多都是拆分成小块进行。存在两个问题
    - 边界伪影问题：patch之间是独立恢复的，拼接时会在边界处出现明显的“接缝”伪影。
    - 边缘像素信息丢失：每个patch的边缘像素，缺乏与邻近patch的上下文信息，影响修复质量。
- **动机**
  - SwinIR 是在 Swin Transformer 基础上，针对图像修复任务（如超分辨率、去噪）设计的模型。将Swin Transformer的思想应用到图像修复任务上。
- **解决思路**
  
  - **利用 Swin Transformer 的思想**
    - 使用窗口注意力+滑动窗口偏移降低计算复杂度，让 Transformer 像 CNN 一样高效处理大尺寸图像。同时可以使得局部Attention 可以跨窗口建模长距离依赖，使其能处理高分辨率图像。
  - **残差连接**
    - 提高训练稳定性
- **具体解决方法**

  - **窗口注意力+滑动窗口**
    - ![image-20250515205002887](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/SwinIR: Image Restoration Using Swin Transformer/image-20250515205002887.png)

  - **残差链接**
    - ![image-20250515205059017](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/SwinIR: Image Restoration Using Swin Transformer/image-20250515205059017.png)

==将Swin Transformer的思想+RCAN(RIR)残差引入图像恢复中，同时解决了CNN感受野有限、分块注意力存在边界伪影和边缘像素信息丢失、全局注意力随尺寸平方增加的问题==



- **上采样部分**

  - **传统SR**

    - ```python
      embed_dim = 96
      num_feat = 64
      ```
      
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
    
  - 轻量化SR
  
    - ```mermaid
      flowchart LR
      	2x[2x]-->D
      	3x[3x]-->D
      	4x[4x]-->D
      subgraph Upsample_RCAN
      		direction LR
      		D[B,96,16,16]-->|conv（96,scale^2）|E[B,scale^2*1,16,16]-->|PixelShuffle（scale）|F[B,1,32,32]
      	end
      ```
  



