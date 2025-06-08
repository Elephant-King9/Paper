**Uformer: A General U-Shaped Transformer for Image Restoration**. Zhendong Wang et.al. **arxiv**, **2021**, ([pdf](assets/pdfs/Uformer:_A_General_U-Shaped_Transformer_for_Image_Restoration.pdf))([link](http://arxiv.org/abs/2106.03106v2)).

- **背景**

  - 为了解决CNN无法建模长距离依赖的问题，且注意力对高分辨率图像代价过高。
- **现有问题**

  - 全局Transformer计算复杂度高，局部感知弱
- **动机**
  - 利用自注意力在多尺度特征图上的能力，以此恢复更多图像细节。

- **解决思路**

  - **UNet结构为基础**	
    - 将UNet中的卷积层替换为Transformer块。
  - **LeWin Transformer Block（局部Transformer）**
    - 解决全局Transformer计算复杂度高 + 局部感知弱两大问题
    - **W-MSA**
      - 将图像划分为不重叠的小窗口（如8×8），只在各窗口内部执行自注意力。避免了全局自注意力的高复杂度（O(N²)）。大幅降低在高分辨率特征图上的计算开销
      - 用UNet结构来弥补窗口交互不足的问题
    - **LeFF**
      - 对标准FFN改进，加入3×3的depth-wise卷积，提升局部感知能力
  - **多尺度空间偏置调制器**
    - 在每个LeWin块的特征上加一个**可学习的窗口级别张量**，提升细节恢复能力。
    - 这种设计简单灵活，几乎不增加额外参数或计算开销。

![image-20250516133032145](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Uformer: A General U-Shaped Transformer for Image Restoration/image-20250516133032145.png)

- **具体解决方法**
  - **LeWin Transformer Block**
    
    - **W-MSA**
      
      - 采用不重叠的窗口内自注意力（Window-based Multi-Head Self-Attention (W-MSA)）。将图像划分为**不重叠的小窗口**（如8×8），只在各窗口内部执行自注意力。避免了全局自注意力的高复杂度（O(N²)）。大幅降低在高分辨率特征图上的计算开销
      - ![image-20250516125829816](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Uformer: A General U-Shaped Transformer for Image Restoration/image-20250516125829816.png)
      
    - **LeFF**
    
      - 在标准Transformer的FFN结构中**加入3×3的depth-wise卷积**，提升局部感知能力（比如边缘、纹理）
    
      - ![image-20250516125842249](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Uformer: A General U-Shaped Transformer for Image Restoration/image-20250516125842249.png)
    
        
    
  - **多尺度空间偏置调制器(Multi-Scale Restoration Modulator)**
    
    - 每个LeWin块内
      - Modulator 是一个 可学习的张量。尺寸为 窗口大小 × 窗口大小 × 通道数。直观上相当于在每个窗口内部加一个可学习的偏置（bias）
    - 在执行窗口内自注意力前，将这个modulator作为共享偏置项添加到每个窗口.这样每个窗口在执行Attention时，会带有一个可调整的偏移，以适应不同退化模式
    - 这种设计简单灵活，几乎不增加额外参数或计算开销。
    - ![image-20250516132251392](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/Uformer: A General U-Shaped Transformer for Image Restoration/image-20250516132251392.png)

==使用Unet+窗口注意力的形式降低了时间复杂度的同时改进了窗口之间的交互问题，定义了全新的FFN，同时在Attention之前增加偏置项适应不同任务==