**Jailbreak and guard aligned language models with only few in-context demonstrations**

- **背景**
- **现有问题**
- **动机**
- **贡献**
- **解决思路**
  - ICA（上下文攻击）
    - 在提示中添加“有害示范”，诱使模型模仿这些例子，从而越狱
    - 即在 prompt 中插入多个会积极响应有害请求的示范，从而诱导模型模仿这些行为（见图1第3个示例）
  - ICD（上下文防御）
    - 在提示中加入“拒绝示范”，引导模型学会拒绝生成有害内容，从而增强安全性
- **具体解决方法**