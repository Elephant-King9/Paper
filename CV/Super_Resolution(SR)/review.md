### 1. (SR)**Image Super-Resolution Using Very Deep Residual Channel Attention Networks**. Yulun Zhang et.al. **arxiv**, **2018**, ([pdf](assets/pdfs/Image_Super-Resolution_Using_Very_Deep_Residual_Channel_Attention__Networks.pdf))([link](http://arxiv.org/abs/1807.02758v2)).
- **RCAN**

- **ECCV:2018**

- **终版提交：2018.7.12**

- **Cite:6048**

- **CNN**

- **现有问题:**深度超分网络难以训练，没有区分不同通道的重要性

- **创新点:==首次提出RIR结构，针对超分辨率深度卷积网络不好训练以及现有模型未能区分高频信息和低频信息的问题，分别提出RIR残差结构和通道注意力进行解决，上采样部分使用低分辨率域处理 + 后期上采样 + 简洁重建来重建==**

- ![image-20250515165929785](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250515165929785.png)

- ![image-20250515165938879](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250515165938879.png)

- [详细信息](./Image Super-Resolution Using Very Deep Residual Channel Attention Networks.md)

### **2. (IR\\SR)SwinIR: Image Restoration Using Swin Transformer**. Jingyun Liang et.al. **arxiv**, **2021**, ([pdf](assets/pdfs/SwinIR:_Image_Restoration_Using_Swin_Transformer.pdf))([link](http://arxiv.org/abs/2108.10257v1)).

- **SwinIR**
- **ICCV:2021**
- **终版提交:2021.8.23**
- **Cite:4123**
- **Transformer**
- **现有问题:**CNN无法捕捉长距离依赖，Transformer能捕捉但是复杂度平方增加，小patch注意力带来的边界伪影与边缘信息丢失问题
- **创新点:==RIR结构，将Swin Transformer的局部注意力与滑动窗口机制引入图像恢复任务，网络设计上借鉴RCAN的残差结构(RIR)，有效缓解了CNN感受野有限、小patch注意力带来的边界伪影与边缘信息丢失问题，同时避免了全局自注意力随图像分辨率平方增长的计算开销。==**
- ![image-20250516132847504](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250516132847504.png)
- [详细信息](./SwinIR: Image Restoration Using Swin Transformer.md)

### 3. (IR)**Uformer: A General U-Shaped Transformer for Image Restoration**. Zhendong Wang et.al. **arxiv**, **2021**, ([pdf](assets/pdfs/Uformer:_A_General_U-Shaped_Transformer_for_Image_Restoration.pdf))([link](http://arxiv.org/abs/2106.03106v2)).

- **UFormer**
- **CVPR:2022**
- **Cite:2016**
- **终版提交:2021.11.25**
- **Transformer**
- **现有问题:**全局Transformer计算复杂度高，局部感知弱
- **创新点:==Unet结构，使用Unet+窗口注意力的形式降低了时间复杂度的同时改进了窗口之间的交互问题，定义了全新的FFN，同时在Attention之前增加偏置项适应不同任务==**
- ![image-20250516124626265](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250516124626265.png)
- [详细信息](./Uformer: A General U-Shaped Transformer for Image Restoration)

### **4. (IR)Restormer: Efficient Transformer for High-Resolution Image Restoration**. Syed Waqas Zamir et.al. **arxiv**, **2021**, ([pdf](assets/pdfs/Restormer:_Efficient_Transformer_for_High-Resolution_Image_Restoration.pdf))([link](http://arxiv.org/abs/2111.09881v2)).

- **Restormer**
- **CVPR:2022**
- **终版提交:2022.3.11**
- **Cite:3133**
- **Transformer**
- **现有问题:**CNN无法捕捉长距离依赖，Transformer能捕捉但是复杂度平方增加，也难以处理高分辨率图像。
- **创新点:==Unet结构，Restormer提出了一种基于通道的注意力机制和改良FFN，结合渐进式学习策略，解决了传统Transformer在高分辨率图像复原中计算复杂度高和内存消耗大的问题。==**
- ![image-20250515183405623](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250515183405623.png)
- [详细信息](./Restormer: Efficient Transformer for High-Resolution Image Restoration.md)

### **5. (SR)Transformer for Single Image Super-Resolution**. Zhisheng Lu et.al. **arxiv**, **2021**, ([pdf](assets/pdfs/Transformer_for_Single_Image_Super-Resolution.pdf))([link](http://arxiv.org/abs/2108.11084v3)).

- **ESRT**
- **CVPRW:2022**
- **终版提交:2022.4.22**
- **Cite:566**
- **Transformer**
- **现有问题:现有SR工作的网路轻量化不足**
- **创新点:==线性结构，提出了新型的网络架构，使用卷积+共享+通道Att，降低通道数，以及注意力图拆分的方式来降低计算量==**
- ![image-20250528223548726](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250528223548726.png)
- [详细信息](Transformer for Single Image Super-Resolution.md)

### **6. (IR\\SR)Cross Aggregation Transformer for Image Restoration**. Zheng Chen et.al. **arxiv**, **2022**, ([pdf](assets/pdfs/Cross_Aggregation_Transformer_for_Image_Restoration.pdf))([link](http://arxiv.org/abs/2211.13654v2)).

- **Cat\Cat_Unet**
- **NIPS:2022**
- **终版提交:2022.5**
- **Cite:193**
- **Transformer**
- **现有问题:**CNN无法捕捉长距离依赖，Transformer能捕捉但是复杂度平方增加，小patch注意力带来的边界伪影与边缘信息丢失问题
- **创新点:==Unet\RIR结构，使用长方形的窗口注意力+偏移来解决现有Transformer的问题，同时在Attention时并行加入卷积来提高学习能力，在IR任务上使用Unet结构，在SR任务上使用RIR结构==**
- ![image-20250516115432877](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250516115432877.png)
- [详细信息](./Cross aggregation transformer for image restoration.md)

### **7. (IR\\SR)Accurate Image Restoration with Attention Retractable Transformer**. Jiale Zhang et.al. **arxiv**, **2022**, ([pdf](assets/pdfs/Accurate_Image_Restoration_with_Attention_Retractable_Transformer.pdf))([link](http://arxiv.org/abs/2210.01427v4)).

- **ART**
- **ICLR:2023**
- **终版提交:2023.2.3**
- **Cite:135**
- **Transformer**
- **现有问题:现有工作(SwinIR、IPT)都是通过减少token数量（patch划分、窗口划分）来降低复杂度，但是每个token始终来自图像的局部密集区域，导致感受野受限，跨区域建模能力差，影响底层视觉任务对全局信息的需求**
- **创新点:==使用RIR结构，在使用了RCAN的残差结构与SwinIR的窗口注意力的基础上，引入SAB来解决窗口Attention无法捕捉长距离依赖的问题==**
- ![image-20250517153230825](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250517153230825.png)
- [详细信息](./Accurate Image Restoration with Attention Retractable Transformer.md)

### 8. (SR)**Activating More Pixels in Image Super-Resolution Transformer**. Xiangyu Chen et.al. **arxiv**, **2022**, ([pdf](assets/pdfs/Activating_More_Pixels_in_Image_Super-Resolution_Transformer.pdf))([link](http://arxiv.org/abs/2205.04437v3)).

- **HAT**
- **CVPR:2023**
- **终版提交：2023.3.19**
- **Cite:933**
- **Transformer**
- **现有问题:**没有人量化解释超分任务中Transformer为什么比CNN更强？同时SwinIR还是存在窗口间交互不足的问题
- **创新点:==采取RIR结构，结合RCAN的全局注意力+SwinIR的W-MSA和SW-MSA+重叠窗口提高信息交互，同时专注于特定任务（进针对SR中的特定倍数分别训练）通过降低泛化性来提高准确性==**
- ![image-20250517173201196](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250517173201196.png)
- ![image-20250517174359919](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250517174359919.png)
- [详细信息](./Activating More Pixels in lmage Super-Resolution Transformer.md)

### **9. (SR)Dual Aggregation Transformer for Image Super-Resolution**. Zheng Chen et.al. **arxiv**, **2023**, ([pdf](assets/pdfs/Dual_Aggregation_Transformer_for_Image_Super-Resolution.pdf))([link](http://arxiv.org/abs/2308.03364v2)).

- **DAT**
- **ICCV:2023**
- **终版提交:2023.8.11**
- **Cite:291**
- **Transformer**
- **现有问题:目前没有工作将窗口注意力和通道注意力相结合**
- **创新点:==RIR结构，同时使用了SwinIR的W-MSA+Restormer的通道注意力，并在Attention时并行加入卷积操作，通过AIM使空间注意力融合通道卷积，通道注意力融合空间卷积，并改进FFN使其能捕捉空间维度的信息==**
- ![image-20250517214520374](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250517214520374.png)
- [详细信息](./Dual Aggregation Transformer for Image Super-Resolution.md)

### 10. (SR)**SRFormerV2: Taking a Closer Look at Permuted Self-Attention for Image Super-Resolution**. Yupeng Zhou et.al. **arxiv**, **2023**, ([pdf](assets/pdfs/SRFormerV2:_Taking_a_Closer_Look_at_Permuted_Self-Attention_for_Image__Super-Resolution.pdf))([link](http://arxiv.org/abs/2303.09735v2))

- **SRFormer**
- **ICCV:2023**
- **终版提交:2023.10.1**
- **Cite:224**
- **Transformer**
- **现有问题:**现有窗口过小，增大窗口又会导致计算量过大
- **创新点:==使用RIR结构,通过对KV的通道压缩和空间重排，来在减小计算量的基础上获得更大的窗口，同时在频域角度讲故事，更新FFN==**
- ![image-20250517230921449](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250517230921449.png)
- [详细信息](./SRFormer: Permuted Self-Attention for Single Image Super-Resolution)

### 11.(SR)Lightweight Image Super-Resolution with Superpixel Token Interaction

- **SPIN**
- **ICCV:2023**
- **终版提交:2023.10.1**
- **Cite:36**
- **Transformer**
- **现有问题:传统窗口注意力划分窗口方式固定，没有考虑到图像本身的关联**
- **创新点:==没有采用RIR结构，纯线性结构。提出聚合窗口策略，通过多次迭代让窗口划分可以根据图像的不同动态改变形状和大小，同时仅选取前N个元素解决每个窗口像素不一致的问题，同时定义新的Att来结合SuperPixel信息与新的FFN来处理信息==**
- ![image-20250518163205990](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250518163205990.png)
- [详细信息](./Lightweight Image Super-Resolution with Superpixel Token Interaction.md)

### 12.**(SR)Transcending the Limit of Local Window: Advanced Super-Resolution Transformer with Adaptive Token Dictionary**. Leheng Zhang et.al. **arxiv**, **2024**, ([pdf](assets/pdfs/Transcending_the_Limit_of_Local_Window:_Advanced_Super-Resolution__Transformer_with_Adaptive_Token_Dictionary.pdf))([link](http://arxiv.org/abs/2401.08209v2)).

- **ADT**
- **CVPR:2024**
- **终版提交:2023.11.15**
- **Cite:39**
- **Transformer**
- **现有问题:**
- **创新点:**
- 
- [详细信息](./Transcending the Limit of Local Window:  Advanced Super-Resolution Transformer with Adaptive Token Dictionary.md)

### 12. (SR)**Multi-scale Attention Network for Single Image Super-Resolution**. Yan Wang et.al. **arxiv**, **2022**, ([pdf](assets/pdfs/Multi-scale_Attention_Network_for_Single_Image_Super-Resolution.pdf))([link](http://arxiv.org/abs/2209.14145v3)).

- **MAN**
- **CVPRW:2024**
- **终版提交:2024.4.13**
- **Cite:81**
- **CNN**
- **现有问题:**CNN全面落后Transformer，挖掘CNN潜质
- **创新点:==RIR架构，CNN网络，旨在追赶CNN与Transformer的差距，对VAN进行改进，引入多尺度大核卷积和门控机制，同时采取类似于Transformer的架构设计，降低了CNN在SR工作上与Transformer的差距，但是在SR的性能上仍小于等于SwinIR( ×2/×3 任务基本持平，x4小于)==**
- ![image-20250518132610031](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250518132610031.png)
- [详细信息](./Multi-scale Attention Network for Single Image Super-Resolution.md)

### 13.**Swift Parameter-free Attention Network for Efficient Super-Resolution**. Cheng Wan et.al. **arxiv**, **2023**, ([pdf](assets/pdfs/Swift_Parameter-free_Attention_Network_for_Efficient_Super-Resolution.pdf))([link](http://arxiv.org/abs/2311.12770v3)).

- **SPAN**
- **CVPRW:2024**
- **终版提交:2024.5.12**
- **Cite:36**
- **CNN**
- **现有问题:**
- **创新点:==设计了一个纯CNN网络，用CNN+非线性来实现SR网络，用非线性的结果与CNN结果相乘来指导特征图更新，来实现用少量参数媲美Attention的效果==**
- ![image-20250603211210948](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250603211210948.png)
- [详细信息](./Swift Parameter-free Attention Network for Efficient Super-Resolution.md)

### **14. (IR)Adapt or Perish: Adaptive Sparse Transformer with Attentive Feature Refinement for Image Restoration**

- **AST**
- **CVPR:2024**
- **终版提交:2024.6.16**
- **Cite:43**
- **Transformer**
- **现有问题:**传统的窗口Attention会和图片中的每一个部分进行计算，但是大部分信息和本像素无关，就造成了需要计算冗余的信息，大量浪费时间在建立与无关信息的联系上
- **创新点:==Unet结构，提出了适应性稀疏自注意力和特征精炼前馈网络FNN，分别在空间和通道维度降低了信息冗余，解决了目前窗口注意力存在信息冗余的问题==**
- **改进想法:==在FRFN中全部通道复制一份，第一份全部保留，第二份稀释==**
- ![image-20250516192606376](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250516192606376.png)
- [详细信息](./Adapt or Perish: Adaptive Sparse Transformer with Attentive Feature Refinement for Image Restoration.md)

### 15. (SR)**Efficient Attention-Sharing Information Distillation Transformer forLightweight Single Image Super-Resolution**. Karam Park et.al. **arxiv**, **2025**, ([pdf](assets/pdfs/Efficient_Attention-Sharing_Information_Distillation_Transformer_for__Lightweight_Single_Image_Super-Resolution.pdf))([link](http://arxiv.org/abs/2501.15774v2)).
- **ASID**

- **AAAI:2025**

- **终版提交:2024.8.19**

- **Cite:2**

- **现有问题:Transformer不够轻量化**

- **创新点:==线性结构，使用了通道注意力+窗口注意力，并使用通道划分蒸馏(区别对待不同重要性的同奥)和Attention权重共享来解决Transformer轻量化的问题==**

- ![image-20250523174631591](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250523174631591.png)

- ![image-20250523174647027](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250523174647027.png)

  

- [详细信息](./Efficient Attention-Sharing Information Distillation Transformer for Lightweight Single Image Super-Resolution.md)

### 16. (SR)**CATANet: Efficient Content-Aware Token Aggregation for Lightweight Image Super-Resolution**. Xin Liu et.al. **arxiv**, **2025**, ([pdf](assets/pdfs/CATANet:_Efficient_Content-Aware_Token_Aggregation_for_Lightweight_Image__Super-Resolution.pdf))([link](http://arxiv.org/abs/2503.06896v1)).
- **CATANet**
- **CVPR:2025**
- **终版提交:2024.11.15**
- **Cite:1**
- **Transformer**
- **现有问题:**现有聚类窗口算法仍有空间优化
- **创新点:==RIR结构,在SPIN的基础上优化聚类窗口注意力，采用单次迭代代替SPIN的多次迭代以提高效率，采用划分子组+子组间注意力的方式来改进SPIN使用Top-K来选择像素导致信息丢失的问题==**
- **问题:==如果同一个窗口像素过多，被分为了多个子窗口(>2个)，在IASA中还是会出现信息交互中断的问题(因为仅与下一个窗口计算注意力，不能与下多个窗口计算注意力)==**
- ![image-20250519173229681](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/review/image-20250519173229681.png)
- [详细信息](./CATANet: Efficient Content-Aware Token Aggregation for Lightweight Image Super-Resolution.md)
