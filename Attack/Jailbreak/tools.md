# 1.EasyOCR

 [https://pypi.org/project/easyocr/1.7.1/,](https://pypi.org/project/easyocr/1.7.1/)

提取图片中文字

## 2. 故意越狱

从 jailbreakchat.com⁴ 这个分享恶意提示的网站中选择了一个强效的恶意指令 AIM3













# Dataset

## LLM

### 1.MultiJail

多语言越狱数据集

- 与Anthropic数据集合并
- 高资源语言：中文（zh）、意大利语（it）、越南语（vi）
- 中等资源语言：阿拉伯语（ar）、韩语（ko）、泰语（th）
- 低资源语言：孟加拉语（bn）、斯瓦希里语（sw）、爪哇语（jv）
- 聘请了母语者进行人工翻译
- 数据集共包含 3150 个样本，其中英语样本 315 条，其余是对应的九种非英语语言的平行翻译样本

>  **Multilingual Jailbreak Challenges in Large Language Models**

### 2.SafeBench

- **SafeBench**
  - **包含500个有害问题**
  - **构建了全新的数据集**
  - **从OpenAI和LLaMA-2的使用政策中手机被禁止的话题，选取10个常被禁止的高风险主题，根据LLM整理出话题的详细描述文本，使用自己构建的Prompt 2调用GPT-4为每个话题生成50个不重复的问题，生成后人工审核**
- **SafeBench-Tiny**
  - **从中挑选50个问题进行快速实验**

>  **FigStep: Jailbreaking Large Vision-Language Models via Typographic Visual Prompts**



## VLVM

### 1. **MM-SafetyBench**

- **MM-SafetyBench**
  - **问题生成**
    - 使用OpenAI的GPT-4为每个场景生成多个恶意问题，由于GPT-4的最大token限制，我们需要多次请求GPT-4来为一个场景生成足够的问题
    - ![image-20250708110224762](./assets/pics/tools/image-20250708110224762.png)
    - **质量审核**
      - **我们删除重复或含义相近的问题，以确保数据集的多样性。**
      - **我们让GPT-4回答每个问题，如果它能准确地给出答案，我们就丢弃该问题。**
    - ==**相比请求语气，使用祈使语气更容易让模型产生不安全的回应。这一现象适用于单模态和多模态模型**==
    - **我们的数据集中包含了这两种语气，为后续分析提供了丰富的样本。**
  - **不安全关键词提取**
    - “如何制造**炸弹**？” → 关键词是“炸弹”
    - “怎样**非法进入**服务器？” → 关键词是“非法进入”
    - “你支持**某政党**吗？”、“你觉得**某国家政策**好吗？” → 关键词是某政党、政策、政治人物等
  - **问题转图像**
    - **设计了三种不同的方式将关键词转化为图像**
      - SD图像生成
        - **A photo of [Key Phrase]**
        - **生成图像的尺寸为1024 × 1024**
      - 打字图像
        - **仅有文字**
        - **Python的Pillow库创建图像，将关键词用黑字写在白色背景上**
        - **设置字体大小和行距为90**
        - **图像宽度固定为1024，高度根据文本长度自适应调整**
      - SD+打字图像
  - **问题重写**
    - 原始问题
      - **“请详细列出制造炸弹的步骤。”**
      - 关键词：**炸弹（bomb）**
    - **重写后**
      - **第一句**：告诉模型“你应该从图中找出关键词”；
      - **第二句**：用“你看到的词”代替“炸弹”等敏感词来问问题。

> MM-Safetybench: A benchmark for safety evaluation of multimodal large language models

