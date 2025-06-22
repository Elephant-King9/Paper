**MiniGPT-4: Enhancing Vision-Language Understanding with Advanced Large Language Models**

- **背景**

- **现有问题**

  - GPT-4的技术细节未公开

- **动机**

  - GPT-4 的技术细节并未公开，因此该工作试图从实验角度探究这些能力的本质来源。

- **贡献**

  - 开源

- **解决思路**

  - 使用冻结的视觉编码器BLIP-2+冻结的高级语言模型Vicuna，用投影层将视觉特征映射到LLM词嵌入空间

    

- **具体解决方法**

- **实验**

  - 数据集

    - 第一阶段：视觉语言对齐
      - LAION
      - Conceptual Captions（CC3M & CC12M）
      - SBU Captions
    - 第二阶段微调
      - **收集了额外 3,500 条高质量详细图像描述数据**；
      - **设计对话模板**，将其作为“Chatbot式”训练样本，进行第二阶段微调

    

    