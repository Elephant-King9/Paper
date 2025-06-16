**A Simple Transformer-style Network for Lightweight Image Super-resolution**

- **背景**
  - 
- **现有缺陷**
  - 但现有的许多高性能方法（如SwinIR、RCAN等）计算代价高、占用内存大，不适合在资源受限的设备上部署。
- **动机**
  - 作者提出了一种简单的“Transformer风格”网络STSN，用于图像超分辨率任务，目标是保留性能的同时降低复杂度。
- **贡献**
  - **提出Conv2FormerB模块**
  - **构建完整STSN**
  - **性能表现优秀+消融实验验证**
- **解决思路**
  -  **Conv2FormerB**
    - **Conv2Former+MLP**
    -  **Conv2Former**
      - 它是一个计算复杂度为线性的结构（Transformer中自注意力是二次复杂度），大大减轻了计算负担
      - Conv2Former 模块用**卷积操作（convolutions）和 Hadamard乘积（逐元素乘法）**来代替传统的自注意力机制，从而简化结构
- **具体解决办法**