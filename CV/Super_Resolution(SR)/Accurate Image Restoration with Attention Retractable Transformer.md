**Accurate Image Restoration with Attention Retractable Transformer**. Jiale Zhang et.al. **arxiv**, **2022**, ([pdf](assets/pdfs/Accurate_Image_Restoration_with_Attention_Retractable_Transformer.pdf))([link](http://arxiv.org/abs/2210.01427v4)).

- **背景**

  - Transformer计算代价高，现有方法（如Swin Transformer）通常采用**不重叠的局部窗口Attention**，限制计算范围，降低复杂度。
  
- **现有问题**
  - 现有工作(SwinIR、IPT)都是通过减少token数量（patch划分、窗口划分）来降低复杂度，但是每个token始终来自图像的局部密集区域，导致感受野受限，跨区域建模能力差，影响底层视觉任务对全局信息的需求
  
- **动机**

  - 解决窗口Attention的交互问题
  
- **解决思路**
  - **RCAN的RIR残差结构**
  - **密集注意力（Dense Attention,DAB）+稀疏注意力（Sparse Attention,SAB）**，**SAB+DAB交替堆叠**
  - **密集注意力（Dense Attention,DAB）**
    - 使用固定、不重叠窗口划分token。这是**传统窗口Attention策略**（类似SwinIR）。
  - **稀疏注意力（Sparse Attention,SAB）**
    - 用**稀疏网格采样**，token来自图像的稀疏区域。这样可以实现跨区域、远距离的token交互。
  - ==**与SwinIR对比**==
  - ![image-20250517150215594](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Accurate Image Restoration with Attention Retractable Transformer/image-20250517150215594.png)
  
- **具体解决办法**

  - **DAB**

    - SwinIR中没有滑动窗口的的窗口注意力
    - ![image-20250517152937819](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Accurate Image Restoration with Attention Retractable Transformer/image-20250517152937819.png)

  - **SAB**

    - 而是以步长为 I 的间隔，在稀疏位置采样token进行交互
    - ![image-20250517152946452](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Accurate Image Restoration with Attention Retractable Transformer/image-20250517152946452.png)

  - **SAB+DAB交替堆叠**

    




![image-20250517153003550](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Accurate Image Restoration with Attention Retractable Transformer/image-20250517153003550.png)

==使用RIR结构，在使用了RCAN的残差结构与SwinIR的窗口注意力的基础上，引入SAB来解决窗口Attention无法捕捉长距离依赖的问题==

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