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

  **==2.引入对比学习(ITC)来指导模型训练==**

  **==3.从头训练，不使用预训练权重==**

  **==4.只保留线性投影==**

  ==**5.简单的数据增强，随机缩放再裁剪**==

  **==6.特征融合简单融合，仅使用点乘（双流架构）导致图文检索任务效果好，但是复杂交互VQA、NLVR2等推理任务上效果不佳==**

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

  ​	**==后续好像证明WPA耗费的资源过大==**

  **==6.指出了双流架构（CLIP）因为仅通过点乘融合特征导致跨模态理解能力有限==**

- ![image-20250620161406285](./assets/pics/review/image-20250620161406285.png)

- [详细信息](./ViLT: Vision-and-Language Transformer  Without Convolution or Region Supervision)


### 3. Align before Fuse: Vision and Language Representation Learning with Momentum Distillation

- **ALBEF**

- **作者: Junnan Li、Ramprasaath R. Selvaraju、Akhilesh D. Gotmare、Shafiq Joty、Caiming Xiong、Steven C.H. Hoi**

- **Salesforce**

- **NIPS:2021**

- **终版提交:2021.05**

- **Cite: 2412**

- **背景**

- **现有问题**

  - **现有模型使用预训练好的目标检测模型提取图像特征，耗时多且不能学习**
  - **现有的数据集要么不够大要么噪声太多**

- **创新点**

  **==1.摒弃目标检测模块，使用预训练好的ViT和BERT初始化权重，Image Embeding>Text Embeding，使用注意力增强特征融合（单流），提高跨模态表征能力==**

  ==**2.使用动量模型（MoCo）来生成对比学习正负样本，同时使用动量模型来对one-hot标签平滑（蒸馏思想）避免因为语义多样性误导学习(MoD)**==

  **==3.使用ITC~MoD~+MLM~MoD~+ITM（softmax第二作为负样本避免崩）==**

  ![image-20250620215345367](./assets/pics/review/image-20250620215345367.png)

- [详细信息](./Align before Fuse: Vision and Language Representation Learning with Momentum Distillation.md)
