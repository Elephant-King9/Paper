**Lightweight Image Super-Resolution with Superpixel Token Interaction**

- **背景**
  - SRCNN首次将CNN引入SR任务重，为了追求性能，RCAN等设计了更深的网络
  - Transformer出现被引入SR重SwinIR基于窗口Attention，ESRT是早起清凉的TransformerSR方法
  - 为了提高效率ELAN引入了分组注意力和贡献股权众
  
- **现有问题**
  - 目前窗口注意力划分方式是固定的，与图像无关，无法解释那些区域该聚合，那些区域不该聚合，就会导致伪影和不同结构区域错误交互
  
- **动机**
  - 解决Patch 分割粗糙和注意力缺乏内容选择性的问题。相比于规则 patch 的“强行划分”，SPIN 的区域是基于像素相似性形成的
  
- **解决思路**
  
  - **引入Superpixel聚合(Superpixel Aggregation,SPA)**
    - 基于**soft k-means** 
    - 超像素基于颜色、纹理、位置等特征进行聚类，可将语义一致的像素自动聚合在一起，形成真正结构完整、纹理连续的区域
  - **Attention(SPCA+ISPA)**
    - **Superpixel Cross-Attention（SPCA）+ 改良FFN**
      - 融入SPA
    - **Intra-Superpixel Attention（ISPA）+ 改良FFN**
      - 使用Top-K选择来解决SPA经过学习后有用像素不一致的问题
  
  
  
- **具体解决方法**

  - **PSA**

    - 将图像划分成n个m*m的小窗格，然后对每个小窗格进行平均池化操作，得到n个聚类中心，然后用n个聚类中心与每一个像素的token算相似度，然后根据计算结果将每个像素重新分配到合适的窗口中，多次迭代就可以让每个聚类中心将原本窗格内同等重要的信息根据关联像素划分重要度，变成视觉上的相关(比如：同一片羽毛、树叶、背景等)

    - ![image-20250518160045717](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Lightweight Image Super-Resolution with Superpixel Token Interaction/image-20250518160045717.png)

  - **SPCA+改良FFN**
    - 将PSA的信息融入
  
    - ![image-20250518161942516](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Lightweight Image Super-Resolution with Superpixel Token Interaction/image-20250518161942516.png)
  
  
  - **ISPA+改良FFN**
  
    - 每个 superpixel 包含的像素数量可能相差很大；
      - 有些 superpixel 边界清晰，只包含少量像素；
      - 有些 superpixel（如背景）很大，包含上百个像素；
  
    - 使用Top-N少选固定每个superpixel的参与像素数量，然后就可以在选定像素上执行标准SA
  
    
  
    - ![image-20250518162446457](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Lightweight Image Super-Resolution with Superpixel Token Interaction/image-20250518162446457.png)

![image-20250518161908922](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Lightweight Image Super-Resolution with Superpixel Token Interaction/image-20250518161908922.png)

==没有采用RIR结构，纯线性结构。提出聚合窗口策略，通过多次迭代让窗口划分可以根据图像的不同动态改变形状和大小，同时仅选取前N个元素解决每个窗口像素不一致的问题，同时定义新的Att来结合SuperPixel信息与新的FFN来处理信息==

- **上采样部分**
  - ```mermaid
    flowchart LR
    	2x[2x]-->D
    	3x[3x]-->D
    	4x[4x]-->H
    subgraph Upsample_RCAN
    		direction LR
    		D[B,40,16,16]-->|conv（40,scale^2*40）|E[B,scale^2*40,16,16]-->|PixelShuffle（upscale）|F[B,40,32,32]-->|RELU|O[B,40,32,32]-->|conv（40,1）|G[B,1,H,W]
    	end
    subgraph Upsample_RCANx2
    		direction LR
    		H[B,40,16,16]-->|conv（40,40*4）|I[B,40*4,16,16]-->|PixelShuffle（2）|J[B,40,32,32]-->|conv（40,40*4）|K[B,40*4,32,32]-->|PixelShuffle（2）|L[B,40,64,64]-->|RELU|N[B,40,64,64]-->|conv（40,1）|M[B,1,H,W]
    	end
    ```