 **CATANet: Efficient Content-Aware Token Aggregation for Lightweight Image Super-Resolution**. Xin Liu et.al. **arxiv**, **2025**, ([pdf](assets/pdfs/CATANet:_Efficient_Content-Aware_Token_Aggregation_for_Lightweight_Image__Super-Resolution.pdf))([link](http://arxiv.org/abs/2503.06896v1)).

- **背景**

  - 虽然CNN开启了SISR的深度学习路径，并通过深层网络扩大感受野以提升性能，但由于其局部感知机制限制了全局建模能力，因此需要牺牲计算效率换取效果，导致实际部署受限。
  - 为降低计算开销，已有工作提出：
    - 分块窗口（如 SwinIR）；
    - 条形窗口（如 axial attention）；
    - 空洞窗口（如 dilated attention）。
  - 
  
- **现有问题**
  - SwinIR的窗口划分是内容无关的，采取固定的窗口(8x8)，会导致重建纹理不一致，伪影，信息利用不充分，条形窗口也不根据内容选择聚焦
  - 为了解决 SPIN 和 ATD 的缺点（建模粗糙、推理慢、计算重）
  
- **动机**
  - 解决内容无感知注意力，与聚类方法(SPIN和ATD)的问题
  
- **解决思路**
  - **RIR结构**
  - **内容感知令牌聚合(Content-Aware Token Aggregation module,CATA）**
    - 通过聚类算法根据图像来动态划分窗口的大小和形状，并通过对窗口再划分成像素数量一致的子窗口来提高并行效率
  
  - **组内自注意力(Intra-Group Self-Attention,IASA)**
    - 解决因为原窗口所含像素过多导致同一个窗口被划分成两个子窗口导致注意力信息中断的问题，同时使用pushback操作解决分组像素乱序的问题
  
  - **本地区域自注意力(Local-Region Self-Attention ,LRSA)**
    - 使用重叠窗口注意力，补充局部区域的详细信息
  
  - **ConvFFN**
    - 通道维度上的特征非线性变化
  
- **具体解决方法**

  - **CATA**
    - 首先将特征图按照窗口划分成M个中心(后续成为窗口区域。假设初始4x4划分，在后续的更新中每个窗口(分组)的大小和形状可能改变，有些窗口(分组)的大小可能变大，可能变小，但是窗口的总数是不变的(始终为M))，随后
      - E-step是根据每个像素（假设共N个）的token来与窗口区域计算余弦相似度，然后将N个token根据相似度归类到M个窗口中（这里分组的组数G等于M个窗口数）
      - M-step是将每一个像素的token分给每个窗口后，对每个窗口重新计算并更新(窗口区域就不限于初始的4x4了，也不一定是矩形了，可能是其他的形状，根据图像进行自适应了)
      - 在更新新的窗口时，EMA的作用是让本次的窗口大小和形状更新时，要记着更新之前窗口的一些信息
    - 这个过程仅一轮，因为在通过上述流程更新完成后，每个窗口所包含的像素数目不同，不利于并行计算，所以通过(b)来对窗口进行重新划分
      - 将像素数不同的M窗口分成多组或者补零来变成Q个新窗口(M<=Q)，每个窗口Q中的像素数量是一致的，便于进行Attention计算
      - 每个子组Q不仅对自己做Attention，并且和下一个子组一起做Attention，这样可以提高组与组之间的信息交互
    - ![image-20250519155913938](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/CATANet: Efficient Content-Aware Token Aggregation for Lightweight Image Super-Resolution/image-20250519155913938.png)
    - ![image-20250519155553940](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/CATANet: Efficient Content-Aware Token Aggregation for Lightweight Image Super-Resolution/image-20250519155553940.png)
  - **IASA**
    - 使用组件交叉注意力来解决同一窗口因为像素过多而被分成两个子窗口，导致信息交互中断的问题，同时使用pushback解决组内信息乱序的问题
  - **LRSA**
    - 使用重叠窗口注意力补充细节信息





![image-20250518144112714](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/CATANet: Efficient Content-Aware Token Aggregation for Lightweight Image Super-Resolution/image-20250518144112714.png)

==在SPIN的基础上优化聚类窗口注意力，采用划分子组+子组间注意力的方式来改进SPIN使用Top-K来选择像素导致信息丢失的问题==

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