### 1. Visual Adversarial Examples Jailbreak Aligned Large Language Models

- **VAE-JLLM**

- **作者: Xiangyu Qi、Kaixuan Huang**

- **Princeton University**

- **AAAI:2024**

- **初版提交: 2023.07.22**

- **Cite: 247**

- **现有问题**

  - 图像是连续的高维数据，相比离散的文本输入，更容易受到对抗攻击（如添加几乎不可察觉的像素扰动）。因此，视觉输入是安全链条中的薄弱环节，大大扩展了模型的攻击面

  - LLMs 能处理的任务多种多样，如问答、推理、生成指令等。这意味着攻击者可以用对抗图像 **实现更多目标**，不只是“分类错误”，还可能引导模型执行恶意操作。

- **贡献**

  - **在多模态背景下揭示了更广泛的攻击面和更严重的安全失败影响**
  - **实证发现一个图像对抗样本可以普遍越狱多个对齐的VLMs，首次将“对抗攻击”问题连接到“AI对齐”的核心挑战上**

- **创新点**

  **==具体流程是使用扰动图片来完成文本的越狱，输入扰动图片和危险文字，通过扰动图片的影响来让VLM输出危险言论==**

  **==1.首次尝试对于VLM进行攻击==**

  **==2.分别测试了扰动图像和扰动文本对于VLM的攻击结果==**

  **==3.使用具体的攻击流程来优化图像扰动==**

- ![image-20250707202158814](./assets/pics/review/image-20250707202158814.png)

- [详细信息](Visual Adversarial Examples Jailbreak Aligned Large Language Models.md)

### 2. FigStep: Jailbreaking Large Vision-Language Models via Typographic Visual Prompts

- **FigStep**

- **作者: Yichen Gong、Delong Ran、Jinyuan Liu、Conglei Wang、Tianshuo Cong、Anyu Wang、Sisi Duan、Xiaoyun Wang**

- **Tsinghua University、Zhongguancun Laboratory、Carnegie Mellon University、National Financial Cryptography Research Center、Shandong Institute of Blockchain、Shandong University**

- **AAAI: 2025 Oral**

- **初版提交: 2023.11.09**

- **Cite: 190**

- **创新点**

  **==认为将文本转化为图像能更好的诱导LVLM出错==**

  **==1.提出了三点直觉==**

  ​	**==模型能看懂图像中的文字==**

  ​	**==图像输入绕过了文字的安全限制==**

  ​	**==让模型“慢慢答”可以进一步欺骗它==**

  **==2.基于这三点直觉使用 改写危险文本=>将改写文本转化为图像，并标出序号=>设计无害的诱导文本让模型输出文字==**

  **==3.创建了新的危险问题数据集SafeBench==**

  **==4.改进版FigStep~adv~:使用扰动图像==**

  **==5.改进版FigStep~hide~:使用图像背景颜色设为 #000010，来绕过OCR==**

- ![image-20250707202112095](./assets/pics/review/image-20250707202112095.png)

- [详细信息](./FigStep: Jailbreaking Large Vision-Language Models via Typographic Visual Prompts.md)