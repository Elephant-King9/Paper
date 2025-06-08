**SRFormerV2: Taking a Closer Look at Permuted Self-Attention for Image Super-Resolution**. Yupeng Zhou et.al. **arxiv**, **2023**, ([pdf](assets/pdfs/SRFormerV2:_Taking_a_Closer_Look_at_Permuted_Self-Attention_for_Image
__Super-Resolution.pdf))([link](http://arxiv.org/abs/2303.09735v2)).

- **背景**

  - 在如SwinIR这类基于窗口自注意力的SR模型中，增加窗口大小可以显著提升性能（因为更大的窗口捕捉到更广泛的上下文信息）。但同时会带来很高的计算开销（注意力的计算复杂度随窗口面积增长）。
- **现有问题**
  - 现有窗口过小，增大窗口又会导致计算量过大

- **动机**
  - 如何在提升Transformer模型性能的同时保持计算效率，尤其是在窗口大小与通道数之间做权衡？**如果我们减小通道数以降低开销，同时扩大窗口来保持感受野，模型的性能会如何变化？**

- **解决思路**
  - **RIR结构**
  - **PSA(通道压缩+空间信息重排)**
    - **通道压缩**
      - Q保持通道数不变，将KV通道压缩，但压缩后存在空间信息损失问题，使用空间信息重排解决
    - **空间信息重排(空间转通道)**
      - 将 K和V的空间维度部分折叠进通道维度
    - 即使窗口增大，计算成本仍低于SwinIR，同时不对窗口进行下采样或者池化，只压缩通道而不是空间，所以每个像素作为独立的token出现，保留了每个像素的独立性
  - **ConvFFN(改进FFN)**
    - 在FFN的两层linear中插入3x3DW-Conv

- **具体解决方法**

  - **PSA+ConvFFN**
  - **即使窗口增大，计算成本仍低于SwinIR**
  - ![image-20250517230938169](/Users/sitianyi/Paper/CV/Restoration/assets/pics/SRFormer: Permuted Self-Attention for Single Image Super-Resolution/image-20250517230938169.png)

![image-20250517225024974](/Users/sitianyi/Paper/CV/Restoration/assets/pics/SRFormer: Permuted Self-Attention for Single Image Super-Resolution/image-20250517225024974-7494962.png)

==使用RIR结构,通过对KV的通道压缩和空间重排，来在减小计算量的基础上获得更大的窗口，同时在频域角度讲故事，更新FFN==

