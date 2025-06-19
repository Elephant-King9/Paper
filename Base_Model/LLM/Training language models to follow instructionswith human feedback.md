**Training language models to follow instructionswith human feedback**

- **背景**
- **现有问题**
- **动机**
  - 希望语言模型更有帮助性、更真诚、无害
- **贡献**
- **解决思路**
  - 手动标了个数据集去通过微调GPT-3
  - 又做了一个排序的数据集，用强化学习训练了一个模型，用于指导GPT-3的生成
  - 结果是只有百分之一的参数量就可以性能优于GPT-3
- **具体解决办法**
- **实验**