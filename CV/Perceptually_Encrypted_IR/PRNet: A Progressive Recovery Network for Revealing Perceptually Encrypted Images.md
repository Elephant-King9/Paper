**PRNet: A Progressive Recovery Network for Revealing Perceptually Encrypted Images**

- **背景**

  - **感知加密**
    - 感知加密通过仅加密对视觉效果至关重要的数据部分来保护图像的视觉内容。
    - 图像被分为重要部分和非重要部分，仅对重要部分进行加密
    - 在密码学中，哪怕能恢复1比特的信息都被认为是安全漏洞；但从图像视觉的角度，这种恢复**并不能带来有意义的视觉泄露**。也就是说，**密码安全 ≠ 视觉安全**
    - ![image-20250608161418998](/Users/sitianyi/Paper/CV/Perceptually_Encrypted_IR/assets/pics/PRNet: A Progressive Recovery Network for Revealing Perceptually Encrypted Images/image-20250608161418998.png)

- **现有问题**

  - 传统密码分析方式（差分攻击、线性攻击）尝试应用于攻击感知加密图像
    - 传统方法依赖对加密算法的“白盒”访问，即必须知道加密过程的全部细节才能进行分析。
    - 这些方法需要手工构造精细的明文-密文对，并对其关系进行分析。这不仅需要大量专业知识，还非常耗时耗力
  - CNN在图像处理中很强大，但是在处理感知加密图像是会有很多挑战
    - 输入图像质量极差，细节严重损坏，导致CNN难以提取有效特征；
    - 加密带来的失真没有规律、分布不均，与常规图像处理中的失真完全不同，使得传统CNN修复方法无法适应。
    - 当面对的是质量极差、失真无规律的加密图像时，这些常规的CNN图像恢复方法就效果不佳甚至无效，无法胜任对加密图像的攻击任务。

- **动机**

  - 将CNN引入加密图像恢复，训练完成后，只需要输入感知加密图像，神经网络即可自动还原出清晰的视觉信息。并且只针对像素本身，而不改变像素的空间位置关系，是一个黑盒+自动化加密图像攻击方法
  - 解决CNN在感知加密中的挑战

- **解决思路**

  - PRNet由多个**密集注意恢复模块（DARB）**组成每个DARB分为两个子模块

    - **特征提取分支（FEB）**
      - 负责从图像中提取多层特征
      - 采用密集链接结构（**DenseNet风格**），解决输入图像质量极差，细节严重损坏问题问题

    - **图像恢复分支（IRB）**
      - 负责根据特征生成中间恢复图像
      - 引入双重显著性机制，从空间和通道维度两方面关注最有意义的信息，解决加密失真无规律、特征提取困难的问题

- **具体解决方法**

  - **DARB**
    - **FEB**
      - 专门负责从图像中抽取有用特征
      - 采用密集卷积链接+局部残差链接
    - **IRB**
      - 专门负责将特征转化为恢复图像
      - 从空间维度和通道维度关注真正有价值的信息
  - ![image-20250608171947157](/Users/sitianyi/Paper/CV/Perceptually_Encrypted_IR/assets/pics/PRNet: A Progressive Recovery Network for Revealing Perceptually Encrypted Images/image-20250608171947157.png)

  - **损失函数**
  - ![image-20250608172210449](/Users/sitianyi/Paper/CV/Perceptually_Encrypted_IR/assets/pics/PRNet: A Progressive Recovery Network for Revealing Perceptually Encrypted Images/image-20250608172210449.png)









![image-20250608171334652](/Users/sitianyi/Paper/CV/Perceptually_Encrypted_IR/assets/pics/PRNet: A Progressive Recovery Network for Revealing Perceptually Encrypted Images/image-20250608171334652.png)

- **实验**

  - **训练集**
    - DIV2K中随机选择300张图像
  - **测试集**
    - Set5、Set12、Kodak24
  - **感知加密方案**
    - **MBSE**
      - 只加密极少量数据以保护图像隐私内容，加密强度低，对视觉影响小。
    - **GLSE**
      - 使用混沌映射生成伪随机序列，对图像的某些比特位进行加密，有一定的加密强度和视觉扰动
    - **RISE**
      - 基于区域重要性，将图像划分成块并选择显著区域进行加密，加密效果强，视觉破坏严重
  - **加密强度等级**
    - **Slight Encryption (SE)**
      - 轻度加密，视觉破坏少；
    - **Moderate Encryption (ME)**
      - 中等强度加密；
    - **Heavy Encryption (HE)**
      - 重度加密，图像视觉严重损坏。

  - **图像尺寸**
    - 32x32

  