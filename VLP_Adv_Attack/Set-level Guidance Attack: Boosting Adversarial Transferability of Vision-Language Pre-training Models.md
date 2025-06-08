**Set-level Guidance Attack: Boosting Adversarial Transferability of Vision-Language Pre-training Models**. Dong Lu et.al. **arxiv**, **2023**, ([pdf](assets/pdfs/Set-level_Guidance_Attack:_Boosting_Adversarial_Transferability_of
__Vision-Language_Pre-training_Models.pdf))([link](http://arxiv.org/abs/2307.14061v1)).

- **背景**

  - VLP模型在图文匹配、视觉问答等任务中对对抗样本是脆弱的（Co-Attack）

- **现有问题**

  - VLP对抗攻击迁移性这一点并没有被系统研究过。

  - 现有方法（Co-Attack）大多只用“单一图文对”来生成对抗样本。生成的对抗样本高度依赖源模型的对齐方式（过拟合到白盒模型的对齐模式）。换个模型后（黑盒场景），这种特定对齐下的扰动很难继续有效，导致迁移性差。

  - ==下图代表模型的迁移性不足==

    

  - ![image-20250515170126659](/Users/sitianyi/Paper/VLP_Adv_Attack/assets/pics/Set-level Guidance Attack: Boosting Adversarial Transferability of Vision-Language Pre-training Models/image-20250515170126659.png)

  - PGD:仅对图像进行扰动

  - BA:BERT-Attack

  - SA:单独对文本和图像分别攻击

  - CA:CO-attack

  - SGA:本模型

- **动机**

  - 探索VLP对抗迁移性

- **造成这一问题的原因**

  - 图片对应多种caption，相当于有很多条路能走，如果攻击只针对其中一种caption（只堵一条路），换个模型可能对齐到其他描述上（走另一条路）

- **解决思路**

  - 对齐保持增强
    - 解决现有对抗攻击方法指导信息单一，导致对抗样本迁移性差、泛化性弱。
    - 通过为每张图片扩展**多匹配caption**与**多尺度图像**，在保持图文对齐的前提下，增加输入数据的多样性，从而生成更具迁移性的对抗样本。

  - 跨模态指导
    - 现有方法缺乏跨模态交互优化，导致对抗样本仅对源模型有效，跨模型迁移时效果大幅下降。
    - 利用**另一模态的配对信息作为监督信号**，通过成组的跨模态交互（图像推离文本、文本推离图像）引导扰动方向，迭代打破对齐关系，生成具有更强迁移性的对抗样本
  - ![image-20250515170139240](/Users/sitianyi/Paper/VLP_Adv_Attack/assets/pics/Set-level Guidance Attack: Boosting Adversarial Transferability of Vision-Language Pre-training Models/image-20250515170139240.png)

- **具体解决方法**

  - 对齐保持增强（成组增强）

    - 对文本：根据一张图片挑选最匹配的多个caption，增强文本指导的多样性

    - 对图像：利用深度模型的尺度不变性，将图片缩放为不同大小，并在此基础上增加高斯噪声

      >  尺度不变性：当输入图像被缩放（变大或变小）后，深度学习模型在识别、匹配、特征提取等任务中仍能保持相对稳定的表现

    - **是“根据一张图片”扩展成一个多样化的集合（图像集合 + caption集合），而不是一组图片作为一个集合**

  - 跨模态指导
    - 对抗caption → 推离原图v
    - 对抗图像v′ → 推离所有对抗caption
    - 最终对抗caption → 再推离对抗图像v′



==首个对于VLP对抗攻击迁移性的研究，通过对齐保持增强和跨模态指导来将单一图片文本扩展成一个集合来进行攻击，进而提升攻击迁移性==