# 1.年份

取arxiv上最早的版本

```mermaid
timeline
    title GAN+VAE+Diffusion
    2013 : Dec
    		 : VAE<br>ICLR 2014<br>Machine Learning Group Universiteit van Amsterdam

    2014 : Jun
    		 : GAN<br>NIPS 2014<br>Universite ́ de Montre ́al
    2015 : Mar
         : Diffusion Model<br>ICML 2015<br>Stanford University
    2017 : Nov
    		 : VQ-VAE<br>NIPS 2017<br>Google DeepMind
    2019 : Jun
    		 : VQ-VAE2<br>NIPS 2019<br>Google DeepMind
    2020 : Jan
    		 : I-GPT<br>ICML 2020<br>OpenAI
    		 : Jun
    		 : DDPM<br>NIPS 2020<br>UC Berkeley
    		 : Oct
    		 : DDIM<br>ICLR 2021<br>Stanford University
    2021 : Feb
    		 : DALL·E<br>ICML 2021<br>OpenAI
    		 : May
    		 : D vs G<br>NIPS 2021<br>OpenAI
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "ICLR 2" : 2
    "NIPS 5" : 5
    "ICML 3" : 3
```

# 3. 关联

黄色代表以VAE为基础的无条件生成模型

绿色代表以Diffusion为基础无条件生成

红色代表VAE基础文本指导的图像生成



-----

**GAN的训练稳定性不强，可能无法覆盖数据分布中的所有模式，但是胜在生成的图像质量较高，在DDPM出现之前性能一直处在生成模型的前列，VAE虽说训练的方法简单但是稳定性较高，缺点是生成图像的质量不如GAN，但是DDPM出现后Diffusion模型又易于训练且恢复图像的质量能达到GAN的性能，知道Diffusion Beat GANs以后Diffusion从数学到性能就完全超越了GAN，至今Diffusion取代了VAE和GAN成为了最好的生成模型**

DDPM 太慢，几十小时才能生成几万张小图，而 GAN 几分钟就搞定。图像越大，DDPM 越慢，要生成大图需要很多天，而 GAN 依然很快。

----

- **变分推断**
  - **为用一个可学习的神经网络去拟合无法计算的数据后验分布**

```mermaid
flowchart BT
VAE-->VQ-VAE
straight-through_estimator-->|离散化梯度传播|VQ-VAE
PixelCNN-->|作为Prior生成器|VQ-VAE
VAE-->|ELBO训练思想|Diffusion_Model
VQ-VAE-->|分层提取<br>两阶段训练|VQ-VAE2
VQ-VAE2-->|两阶段训练+CodeBook+ELBO|DALL-E
I-GPT-->|Transformer引入|DALL-E
Gumbel-softmax-->|解决离散梯度不可导|DALL-E
Diffusion_Model-->|逐步优化策略|DDPM
DDPM-->|优化生成时间|DDIM




VAE[VAE（2013.12）<br>使用原图映射到隐空间<br>从隐空间随机抽样生成图像]
	style VAE fill:#F3D266
VQ-VAE[VQ-VAE（2017.11）<br>引入CodeBook离散化，来解决VAE生成聚类的问题<br>首次提出两阶段训练方式]
	style VQ-VAE fill:#F3D266
VQ-VAE2[VQ-VAE2（2019.06）<br>VQ-VAE的基础上分层提取<br>分别提取高层和底层信息]
	style VQ-VAE2 fill:#F3D266
DALL-E[DALL·E（2021.02）<br>文本指导图像生成<br>引入Transformer Decoder，使用掩码学习]
	style DALL-E fill:#EF7A6D
I-GPT[iGPT（2020.01）<br>Transformer引入生成模型]
Gumbel-softmax[Gumbel-softmax]
Diffusion_Model[Diffusion Model（2015.03）<br>Diffusion模型理论基础<br>仅在小规模数据集上训练]
	style Diffusion_Model fill:#63E398
DDPM[DDPM（2020.06）<br>将预测图像转化为预测噪声<br>简化了损失公式<br>可以在训练加噪随时生成时间为T的噪声，不需要马尔科夫逐渐推导]
	style DDPM fill:#63E398
DDIM[DDIM（2020.10）<br>通过去除马尔科夫链来加快生成图像的时间]
	style DDIM fill:#63E398
```





# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [VAE,GAN,DM,VQ-VAE,VQ-VAE2,I-GPT,DDPM,DDIM,DALL-E,D vs G]
    y-axis "Cite" 
    bar [46034, 83283, 8634,6258, 2329, 2050, 23847, 8896,6536, 9492]
    line [46034, 83283, 8634,6258, 2329, 2050, 23847, 8896,6536, 9492]
```



