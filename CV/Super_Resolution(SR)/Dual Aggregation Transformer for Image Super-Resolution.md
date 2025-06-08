**Dual Aggregation Transformer for Image Super-Resolution**. Zheng Chen et.al. **arxiv**, **2023**, ([pdf](assets/pdfs/Dual_Aggregation_Transformer_for_Image_Super-Resolution.pdf))([link](http://arxiv.org/abs/2308.03364v2)).

- **背景**

  - 现有Transformer方法通常在**空间维度（Spatial）**或**通道维度（Channel）**上使用自注意力。并且取得了优秀性能。

  - 在空间维度：

    - 方法如SwinIR、CSWin等通过**局部窗口自注意力（Spatial Window Self-Attention, SW-SA）**降低计算复杂度。
    - 只在局部窗口内计算SA，牺牲部分全局信息以提升效率。

  - 在通道维度：

    - 方法如Restormer引入了**转置注意力（Transposed Attention）**。
    - 在**通道维度而不是空间维度**计算SA，能够高效建模通道间的全局关系，代价较低。

- **现有问题**

  - 现有工作没有结合通道和空间注意力
- **动机**

  - SW-SA和CW-SA各有优势且互补将空间和通道两个维度的自注意力结合，可能进一步增强特征表示能力。

- **解决思路**
  - **RIR网络结构**
  - **自适应空间自我注意力(Adaptive spatial self-attention,AS-SA)+自适应通道自我注意力(AC-SA)**
    - **AS-SA**
      - **SwinIR的SW-MSA+AIM+并行卷积**
      - 引入并行卷积提高捕获全局信息的能力

    - **AC-SA**
      - **Restormer的通道注意力+AIM+并行卷积**
      - 引入并行卷积提高捕获全局信息的能力

    - **AIM**
      - 判断当前为WA还是CA
        - WA则将并行卷积转化为通道形式融合
        - CA则将并行卷积转化为空间形式融合

  - **改良FFN(Spatial-Gate Feed-Forward Network,SGFN)**
    - 传统FFN无法捕捉空间信息（像素之间的关系）
    - SGFN能够建模空间信息。同时通过通道分割+门控减轻通道冗余。

- **具体解决方法**
  - **AS-SA+AC-SA**
    - 在Attention时并行加入卷积，同时判断当前是SA还是CA
      - SA，则并行卷积转化为通道结合
      - CA，则并行卷积转化为空间结合

    - ![image-20250517213151382](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Dual Aggregation Transformer for Image Super-Resolution/image-20250517213151382.png)

  - **SGFN**
    - ![image-20250517213656582](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Dual Aggregation Transformer for Image Super-Resolution/image-20250517213656582.png)

![image-20250517214543126](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Dual Aggregation Transformer for Image Super-Resolution/image-20250517214543126.png)

- **上采样部分**

  - 通道部分有所变动，初始embed_dim从传统的96到了180

  - ```mermaid
    flowchart LR
    	subgraph conv_before_upsample
    		direction LR
    		A[B,180,16,16]-->|conv（180,64）|B[B,64,16,16]-->|RELU|C[B,64,16,16]
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
      		D[B,180,16,16]-->|conv（180,scale^2*1）|E[B,scale^2*1,16,16]-->|PixelShuffle（2）|F[B,1,32,32]-->|conv（64,1）|G[B,1,H,W]
      	end
      ```
  
    
  
    



==RIR结构，同时使用了SwinIR的W-MSA+Restormer的通道注意力，并在Attention时并行加入卷积操作，通过AIM使空间注意力融合通道卷积，通道注意力融合空间卷积，并改进FFN使其能捕捉空间维度的信息==