**Understanding Robust Overfitting in Adversarial Training of GNNs: A Stability and Generalization Perspective**

- **背景**

  - 对抗训练是提升 GNN 抵抗攻击能力的主流方法，但它会导致模型在训练时对抗样本表现很好，但在测试时效果变差（即在对抗样本上的过拟合）
  - 这可能是因为：对抗损失函数本身是非平滑的（non-smooth），导致优化不稳定
    - **光滑（smooth）**：指的是函数具有良好的数学性质，例如一阶或二阶连续可导，曲线平滑，没有尖点或断点。
    - **非光滑（non-smooth）**：表示函数中可能存在尖角、不可导点，梯度变化剧烈或不连续。
    - 对抗训练过程是一个 **max-min 优化**（先最大化扰动，再最小化损失），它会导致最终的损失函数相较于干净训练的损失函数“更不规则”
  
- **现有问题**
  - 图神经网络容易受到对抗攻击，尤其是在白盒设置下
  
    - 即使是微小的图结构扰动（如添加/删除一条边），都可能极大改变信息传播路径，造成预测误差。
  
  - 对抗训练会出现鲁棒性过拟合的问题
  
    - 模型在训练阶段可以很好地拟合对抗样本，但在测试阶段，对抗鲁棒性反而变差
    - 模型过度拟合训练扰动，而失去了泛化能力。
  
  - 白盒攻击的一大挑战
  - 损失函数非光滑，攻击依赖梯度最大化，导致整体的损失函数非光滑，即使平滑标准损失，也无法解决非光滑问题
  
- **现有工作**
  
  - **基于特征攻击的对抗训练方法**
    - **FLAG**
      - Robust optimization as data augmentation for large-scale graphs.(2019)
      - 多次迭代对节点特征增加扰动，增强GNN的鲁棒性
    - **BVAT**
      - Batch virtual adversarial training for graph convolutional networks.(2023)
      - 引入虚拟对抗扰动(VAT)，通过扰动节点特征来提升模型输出的平滑性
  - **基于结构攻击的对抗训练方法**
    - **基于图扩散模型（diffusion model）的GNN结构**
      - Adversarial training for graph neural networks: Pitfalls, solutions, and new directions.(2024)
    - **图子空间能量（Graph Subspace Energy）来度量扰动影响**
      - Adversarial training for graph neural networks via graph subspace energy optimization.(2024)
    - **零阶优化（Zeroth-order Optimization）方法，用于无梯度的对抗训练**
      - Topology attack and defense for graph neural networks: An optimization perspective.(2019)
  
- **动机**

  - **从稳定性角度解释并缓解过拟合**
  - **理论角度分析了GNN在白盒与黑盒对抗训练场景下的稳定性与泛化性**
  
- **解决思路**
  - **“uniform stability”（统一稳定性）理论**

  - 利用已有的“uniform stability（统一稳定性）”理论，**来系统性分析图神经网络（GNN）在对抗训练过程中出现的鲁棒过拟合问题**，并评估不同训练策略（如SGD、随机平滑、Moreau平滑、黑盒优化）的泛化能力。

- **具体解决方法**







==用一个现有的方法来从理论方向分析关于GNN对抗训练的问题的论文==





- 缺乏理论创新，过于依赖已有工具，主要是套用已有工具来分析目前现有的对抗训练网络，创新性较差











