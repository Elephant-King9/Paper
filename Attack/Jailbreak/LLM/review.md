### 1. AUTOPROMPT: Eliciting Knowledge from Language Models  with Automatically Generated Prompts

- **AutoPrompt**

- **作者: Taylor Shin、Yasaman Razeghi、Robert L. Logan IV、Eric Wallace、Sameer Singh**

- **University of California**

- **初版提交:2022.10.31**

- **Cite: 2157**

- **背景**

- **现有问题**

  - 预训练语言模型不清楚是预训练学到了知识还是微调学到的
  - 使用人工prompt的方法可能无法让模型理解意图，导致有知识但是说不出来的问题

- **贡献**

  - **创建了一种自动生成prompt来评估预训练语言模型性能的模型**

- **创新点**

  **==1.创建了一种生成prompt的方法，能够更好的帮助预训练语言模型(BERT)模型理解问题，让BERT能把自己的知识更好的表示出来来帮助人们测试预训练模型的知识学习程度==**

- ![image-20250624144837143](./assets/pics/review/image-20250624144837143.png)

- [详细信息](./AUTOPROMPT: Eliciting Knowledge from Language Models  with Automatically Generated Prompts.md)

### 2. MasterKey: Automated Jailbreak Across Multiple Large Language Model Chatbots

- **MasterKey**

- **作者: Gelei Deng、Yi Liu、Yuekang Li、Kailong Wang、Ying Zhang、Zefeng Li、Haoyu Wang、Tianwei Zhang、Yang Liu**

- **Nanyang Technological University、University of New South Wales、Huazhong University of Science and Technology、Virginia Tech**

- **NDSS:2024**

- **初版提交: 2023.07.16**

- **Cite: 213**

- **创新点**

  **==1.通过时间SQL注入的思想判断了目前黑盒模型是如何检测危险输出的==**

  **==2.通过设计数据增强，将现有的LLM微调成生成越狱文本的LLM，并通过奖励机制优化==**

- ![image-20250706212636244](./assets/pics/review/image-20250706212636244.png)

- ![image-20250706212646384](./assets/pics/review/image-20250706212646384.png)

- [详细信息](./MasterKey: Automated Jailbreak Across Multiple Large Language Model Chatbots.md)

### 3. Universal and Transferable Adversarial Attacks  on Aligned Language Models

- **GCG**

- **作者: Andy Zou、Zifan Wang、Nicholas Carlini、Milad Nasr、J. Zico Kolter、Matt Fredrikson**

- **Carnegie Mellon University、Center for AI Safety、Google DeepMind、Bosch Center for AI**

- **初版提交: 2023.07.27**

- **Cite: 1631**

- **背景**

  - LLMs 是在大量从互联网上抓取的文本语料上训练的。这些数据中不可避免地包含了大量不良内容
  - 相比图像任务，自动搜索算法生成 adversarial prompts（如使用梯度搜索、强化学习等）在文本领域效果较差，难以稳定实现

- **现有问题**

  - 尽管已有“越狱攻击（jailbreak）”可以绕过对齐策略，但这些方法：
    - 依赖大量人工提示设计（human ingenuity）
    - 可迁移性差，容易失效（brittle）

  - 以往工作也尝试过类似方式（例如 Carlini et al., 2023），但：
    - 往往不稳定、成功率低，即使在白盒条件下也难以稳定越狱；
    - 原因是缺乏有效的目标函数（loss）、数据处理方式、优化策略等关键设计。
  - AutoPrompt：每次只优化一个 token 位置（一个“coordinate”）。
    - 它先选定某个位置，比如 prompt 第 2 个词；
    - 然后只尝试替换这个位置的 token。

- **贡献**

  - **提出一种可自动生成、通用、可迁移的越狱攻击方法。不改变初始问题，而是在初始问题后添加对抗prompt来实现越狱**
  - **显著提升了当前对齐语言模型攻击的效果。**
  - **揭示了对齐机制在多模态 LLM 中的脆弱性，引发了对未来对抗防御的反思。**

- **创新点**

  **==1.提出了一种目标函数的方法用于训练，将让模型生成”Sure,here is how to + 问题本身“作为优化目标==**

  **==2.提出了一种全新的优化策略，更新对抗prompt使用Top-K根据损失在固定的字典中选取单词，而不是整个空间==**

  **==3.指出针对多问题越狱时，初始先对单问题越狱，越狱成功后再逐一添加的效果更好==**

- ![image-20250623180928007](./assets/pics/review/image-20250623180928007.png)

- [详细信息](./Universal and Transferable Adversarial Attacks on Aligned Language Models.md)

### 4. Gpt-4 is too smart to be safe: Stealthy chat with llms via cipher

- **CipherChat**

- **作者: Youliang Yuan、Wenxiang Jiao、Wenxuan Wang、Jen-tse Huang、Pinjia He、Shuming Shi、Zhaopeng Tu**

- **The Chinese University of Hong Kong、Tencent AI Lab**

- **ICLR: 2024**

- **初版提交: 2023.08.12**

- **Cite: 284**

- **创新点**

  **==1.CipherChat：将普通语言转化为加密语言（如ASCII）然后让模型用加密语言回答危险问题再翻译回来==**

  **==2.SelfCipher：让模型模拟一个未知的语言，但是还是用英文回答，但是模型会以为危险的英文言论是正常的加密语言，从而回答==**
  
- ![image-20250706193926289](./assets/pics/review/image-20250706193926289.png)

- [详细信息](./Gpt-4 is too smart to be safe: Stealthy chat with llms via cipher.md)

### 5. Autodan: Generating stealthy jailbreak prompts on aligned large language models

- **AutoDAN**

- **作者: Xiaogeng Liu、Nan Xu、Muhao Chen、Chaowei Xiao**

- **University of Wisconsin–Madison、USC、University of California**

- **ICLR: 2024**

- **初版提交: 2023.10.03**

- **Cite: 636**

- **创新点**

  **==1.使用GCG的优化目标，使用遗传算法来生成越狱提示，相比于GCG生成的越狱提示更具有可读性==**

- ![image-20250707183645215](./assets/pics/review/image-20250707183645215.png)

- ![image-20250707183656366](./assets/pics/review/image-20250707183656366.png)

- [详细信息](./Autodan: Generating stealthy jailbreak prompts on aligned large language models.md)

### 6. Jailbreak and guard aligned language models with only few in-context demonstrations

- **ICA/ICD**

- **作者: Zeming Wei、Yifei Wang、Ang Li、Yichuan Mo、Yisen Wang**

- **Peking University、MIT CSAIL**

- **初版提交: 2023.10.10**

- **Cite: 300**

- **创新点**

  **==1.提出了使用类似one-shot的方法，先给出一个回答危险问题的例子，然后问模型新的危险问题，模型根据one-shot的例子就会回答==**

  **==2.对于防御部分，先给出模型拒绝回答危险问题的例子，然后让模型拒绝回答新的危险问题==**

  **==3.分析了这种情况为什么会出现==**

- ![image-20250707190748394](./assets/pics/review/image-20250707190748394.png)

- [详细信息](./Jailbreak and guard aligned language models with only few in-context demonstrations.md)

### 7. Multilingual Jailbreak Challenges in Large Language Models

- **MultiLingual**

- **作者: Yue Deng、Wenxuan Zhang、Sinno Jialin Pan、Lidong Bing**

- **DAMO Academy、Nanyang Technological University、Hupan Lab、The Chinese University of Hong Kong**

- **ICLR:2024**

- **初版提交: 2023.10.10**

- **Cite: 282**

- **创新点**

  **==1.探究了不同语言的相同文字的越狱结果==**

  **==2.构建了数据集MultiJail，多语言的危险问题==**

  **==3.构建了防御措施Self-Defence，通过安全语言+危险问题的不同语言微调大模型==**

- ![image-20250707201154295](./assets/pics/review/image-20250707201154295.png)

- [详细信息](./Multilingual Jailbreak Challenges in Large Language Models.md)

### 8. DeepInception: Hypnotize Large Language Model to Be Jailbreaker

- **DeepInception**

- **作者: Xuan Li、Zhanke Zhou、 Jianing Zhu、Jiangchao Yao、Tongliang Liu、Bo Han**

- **Hong Kong Baptist University、Shanghai Jiao Tong University、Shanghai AI Laboratory、The University of Sydney**

- **NIPS workshop: 2024**

- **初版提交: 2023.11.06**

- **Cite: 216**

- **创新点**

  **==1.引诱大模型进行角色扮演，并通过多轮问答诱导越狱==**

- ![image-20250706200917560](./assets/pics/review/image-20250706200917560.png)

- [详细信息](DeepInception: Hypnotize Large Language Model to Be Jailbreaker.md)
