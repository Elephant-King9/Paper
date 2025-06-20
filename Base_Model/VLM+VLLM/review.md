### 1. Learning Transferable Visual Models From Natural Language Supervision

- **CLIP**

- **作者: Alec Radford 、Jong Wook Kim、Ilya Sutskever**

- **OpenAI**

- **终版提交: 2021.1**

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

  **==1.首个使用文本指导图像学习且Zero-Shot效果很好的模型，让分类任务不局限于给定的分类，提高了迁移性==**

  **==2.引入对比学习来指导模型训练==**

  **==3.从头训练，不使用预训练权重==**

  **==4.只保留线性投影==**

  ==**5.简单的数据增强，随机缩放再裁剪**==

- ![image-20250620141739370](./assets/pics/review/image-20250620141739370.png)

- [详细信息](./Learning Transferable Visual Models From Natural Language Supervision.md)

