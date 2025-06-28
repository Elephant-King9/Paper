### **1. Auto-Encoding Variational Bayes**

- **VAE**

- **作者:Diederik P. Kingma、Max Welling**

- **Machine Learning Group Universiteit van Amsterdam**

- **ICLR: 2014**

- **初版提交: 2013.12.20**

- **Cite: 46034**

- **背景**

- **现有问题**

- **贡献**

- **创新点**

  ==**1.创建了损失函数和梯度优化的方式，能够训练一个从初始图像x到特征z，再根据一个随机的特征z生成新的图形x的模型**==

- ![image-20250626162146788](./assets/pics/review/image-20250626162146788.png)

- **[详细信息](./Auto-Encoding Variational Bayes.md)**

### 2. Generative Adversarial Nets

- **GAN**

- **作者: Ian J. Goodfellow、Jean Pouget-Abadie、Mehdi Mirza、Bing Xu、David Warde-Farley、Sherjil Ozair、Aaron Courville、Yoshua Bengio**

- **Universite ́ de Montre ́al**

- **NIPS: 2014**

- **初版提交: 2014.06.10**

- **Cite: 83283**

- **背景**

- **现有问题**

  - 以前的方法总想着去构造一个分布函数出来，然后让这个函数提供一些可学习参数，通过最大化似然函数来优化

    - 好处是知道是什么分布，均值方差等很清晰
    - 缺点是当纬度较高的时候计算困难
    - 相当于我游戏生成出了画面，我通过反编译得到游戏的源码来重新生成游戏画面

  - 最近出来了新的方法"generative machines"(GAN,VAE)，不构造分布，而是构建一个模型去近似分布

    - 好处是学习简单，对期望求导等于对函数本身求导
    - 缺点是不知道具体的分布是什么
    - 相当于游戏生成了画面，我用另一个游戏程序去模拟画面生成，我还是不知道当前生成画面的游戏的代码，但是我能生成和这个游戏差不多的画面

    - 这个就是类似于使用一组数据反推函数，方法A完全知道这条函数的表达式，方法B是拟合模型

- **创新点**

  **==1. 提出了对抗生成网络，通过生成器生成以假乱真的图片，判别器辨别是真实图片还是生成图片，两个网络协同更新，最终达到生成器以假乱真的效果==**

- ![image-20250628161311272](./assets/pics/review/image-20250628161311272.png)

- [详细信息](./Generative Adversarial Nets.md)

### 3. Neural Discrete Representation Learning

- **VQ-VAE**

- **作者: Aaron van den Oord、Oriol Vinyals、Koray Kavukcuoglu**

- **Google DeepMind**

- **NIPS: 2017**

- **初版提交: 2017.11.02**

- **Cite: 6258**

- **背景**

- **现有问题**

  - VAE生成图片因为强大的生成器导致只生成几类图片的问题，生成的图片随机性下降

- **创新点**

  **==1.将VAE中的隐空间离散化，避免了生成图片因为强大的生成器导致只生成几类图片的问题==**

  **==2.维护了一个codebook，让图像映射到连续的向量空间中时，对每个特征与codebook中的向量进行比对，然后用离散的codebook代替初始连续的特征==**

  **==3.在生成过程使用了自回归的方式(类似LLM)，首先从离散的Codebook上随机选择一个特征，其后选择的特征都根据前面已经选择的特征计算概率然后根据概率抽样，来完成随机选择的过程==**

- ![image-20250628175130172](./assets/pics/review/image-20250628175130172.png)

- [详细信息](./Neural Discrete Representation Learning.md)

### 4. Generating Diverse High-Fidelity Images with VQ-VAE-2

- **VQ-VAE2**

- **作者: Ali Razavi、Aäron van den Oord、Oriol Vinyals**

- **Google DeepMind**

- **NIPS: 2019**

- **初版提交: 2019.06.02**

- **Cite: 2329**

- **背景**

- **现有问题**

- **创新点**

  **==1.在VQ-VAE的基础上分层生成字典，可以捕获更多的图像信息==**

- ![image-20250628195940662](./assets/pics/review/image-20250628195940662.png)

- [详细信息](./Generating Diverse High-Fidelity Images with VQ-VAE-2.md)
