### 1. Learning Transferable Visual Models From Natural Language Supervision

- **CLIP**

- **作者: Alec Radford 、Jong Wook Kim、Ilya Sutskever**

- **OpenAI**

- **ICML:2021**

- **终版提交: 2021.01**

- **Cite: 36752**

- **背景:**
  - 基于纯文本预训练+零样本适配下游任务的统一语言模型推动了NLP进入任务无关，零样本迁移的新时代
  - 在NLP领域 大数据弱监督>小数据强监督
  - 在CV领域预训练仍然高度依赖人工标注

- **现有问题:**传统的计算机视觉模型（分类器）只能识别固定的一组标签，但是现有任务的文本指导图像识别参数量和数据量又不够

- **贡献:**

  - **1.利用自然语言监督信号定义全新的分类器，实现Zero-Shot学习**
  - **2.将大量参数和数据引入指导学习**

- **创新点:**

  **==文本:Transformer 图像:ResNet or ViT==**

  **==1.首个使用文本指导图像学习且Zero-Shot效果很好的模型，让分类任务不局限于给定的分类，提高了迁移性==**

  **==2.引入对比学习来指导模型训练==**

  **==3.从头训练，不使用预训练权重==**

  **==4.只保留线性投影==**

  ==**5.简单的数据增强，随机缩放再裁剪**==

- ![image-20250620141739370](./assets/pics/review/image-20250620141739370.png)

- [详细信息](./Learning Transferable Visual Models From Natural Language Supervision.md)

### 2. ViLT: Vision-and-Language Transformer  Without Convolution or Region Supervision

- **ViLT**

- **作者: Wonjae Kim、Bokyung Son、Ildoo Kim**

- **韩国Kakao公司**

- **ICML:2021**

- **终版提交:2021.01**

- **Cite:2115**

- **背景:**现有的VLP模型，在处理图文任务时通常采用预训练的图像编码器来提取图像中的目标(目标检测)，然后将图像特征和文本输入送入一个 Transformer 模块进行跨模态融合。

- **现有问题:**模型不够轻量化，大部分对于图像的操作太冗余，或者是在特征融合部分效果不好

- **创新点:**

  **==1.对现有模型进行轻量化，首次尝试了图像ViT+文本Transformer(单流架构)==**

  **==2.提出了图像增强和整词MASK的训练策略==**

  **==3.对现有工作进行了总结==**

  **==4.摒弃了目标检测模块，提高了模型效率==**

  **==5.除了ITM+MLM+WPA损失==**

- ![image-20250620161406285](./assets/pics/review/image-20250620161406285.png)

- [详细信息](./ViLT: Vision-and-Language Transformer  Without Convolution or Region Supervision)

  

