### 1. Extracting Training Data from Diffusion Models

- **DS**

- **作者: Nicholas Carlini、Jamie Hayes、Milad Nasr、Matthew Jagielski、Vikash Sehwag、Florian Tramer、Borja Balle、Daphne Ippolito、Eric Wallace**

- **Google DeepMind**

- **USENIX: 2023**

- **初版提交: 2023.01.30**

- **Cite: 803**

- **创新点**

  **==1.评估了Stable Diffusion的数据安全问题，并进行实验判断Diffusion模型是真的能够创新还是仅临摹==**

  **==2.通过改进的欧几里得二范数距离^[5]^来衡量生成图像和数据集图像的相似度来判断模型是否有真的记忆==**

  **==3.对于白盒数据窃取，使用了成员推理攻击和属性推理攻击来攻击自己训练基于CIFAR-10 Diffusion==**

  **==4.提出了几种能防止Diffusion数据窃取的方法==**

- [详细信息](./Extracting Training Data from Diffusion Models.md)