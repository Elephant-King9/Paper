**Activating More Pixels in Image Super-Resolution Transformer**. Xiangyu Chen et.al. **arxiv**, **2022**, ([pdf](assets/pdfs/Activating_More_Pixels_in_Image_Super-Resolution_Transformer.pdf))([link](http://arxiv.org/abs/2205.04437v3)).

- **背景**

  - Transformer方法已经在低层视觉任务（如图像超分辨率）中取得了优秀的表现。

    - **SwinIR**（基于Swin Transformer的SR方法）取得了**SR任务的突破性提升**。
    - 成为**Transformer在SR领域的代表性方法**。

    

- **现有问题**

  - 1. **没有人量化解释超分任务中Transformer为什么比CNN更强？**

    - 一个直观的解释是Transformer依靠自注意力机制。理论上可以建模长距离依赖，利用更多远距离信息。但是没有人真正的分析Transformer为什么比CNN更强
    
    - 作者在使用LAM（Local Attribution Map）进行分析后，发现SwinIR与RCAN使用信息范围相近，说明现有Transformer潜力还没有被充分挖掘，只能利用到有限的空间范围信息。
    
    - > 这是一种**归因分析方法**，可以分析模型在预测时究竟使用了输入图像的哪些区域
    
    - ![image-20250517170344854](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Activating More Pixels in lmage Super-Resolution Transformer/image-20250517170344854.png)

  - 2. **SwinIR的中间特征图中出现了块状伪影（Blocking Artifacts）说明Shifted Window机制，在跨窗口信息交互上存在不足**

  - ![image-20250517170116424](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Activating More Pixels in lmage Super-Resolution Transformer/image-20250517170116424.png)

  - 3. **Transformer缺少像CNN那样的感受野局部性、平移等变性等内在归纳偏置。**

    - 因此，Transformer往往需要更大规模的数据预训练，才能发挥其潜力。

- **动机**

  - 保留自注意力优势，同时激活更多像素参与重建，并解决SwinIR滑动窗口仍存在边界伪影的问题

- **解决思路**

  - **RIR的网络结构**

  - **通道注意力+ 基于窗口的自注意力+重叠跨窗口注意力（Overlapping Cross-Attention）**
     -  **通道注意力（RCAN,Channel Attention,CA）**
        -  善于建模全局统计信息（全图范围统计），可以激活更多像素
     -  **基于窗口自注意力（SwinIR,Window-based Self-Attention，W-MSA）**
        -  擅长局部区域拟合（细节、纹理）
     -  **重叠跨窗口注意力（Overlapping Cross-Attention,OCA）**
        -  增强相邻窗口之间的直接交互,解决SwinIR中的块状伪影问题(Shift Window机制跨窗口信息流通不充分)。

  - **同任务预训练（Same-task Pre-training）**
    - 即在相同任务（如超分）上进行大规模预训练,不像其他方法那样多任务或多退化混合。

- **具体解决办法**

  - **网络结构:通道注意力+基于窗口自注意力**
    - HAB中交替使用窗口注意力(W-MSA)和移动窗口注意力(SW-MSA),同时并行链接CAB(类似于RCAN)增强全局捕捉能力
    - ![image-20250517173150854](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Activating More Pixels in lmage Super-Resolution Transformer/image-20250517173150854.png)

  - **OCA**

    - 不对称窗口划分

    - 采用重叠的窗口，涵盖了更大的感受野，跨越了多个相邻窗口

    - ![image-20250517174304865](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Activating More Pixels in lmage Super-Resolution Transformer/image-20250517174304865.png)


  - **同任务预训练（Same-task Pre-training）**

    - **专注于同一个任务（如4倍超分），直接在大规模数据（ImageNet）上进行预训练**。
    - 不做多任务，也不做多退化。

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

    


==采取RIR结构，结合RCAN的全局注意力+SwinIR的W-MSA和SW-MSA+重叠窗口提高信息交互，同时专注于特定任务通过降低泛化性来提高准确性==

