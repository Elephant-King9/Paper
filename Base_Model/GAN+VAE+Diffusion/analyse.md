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
    		 : Improved DDPM<br>ICML 2021<br>OpenAI
    		 : DALL·E<br>ICML 2021<br>OpenAI
    		 : May
    		 : ADM<br>NIPS 2021<br>OpenAI
    		 : CogView<br>NIPS 2021<br>Tsinghua University
    		 : Dec
    		 : GLIDE<br>OpenAI
    		 : Stable Diffusion<br>CVPR 2022<br>Ludwig Maximilian University of Munich & Heidelberg University
    2022 : Apr
    		 : DALL·E2<br>OpenAI
    		 : May
    		 : Imagen<br>NIPS 2022<br>Google Brain
    		 : Jul
    		 : Classifier-Free Diffusion<br>Google Brain
    		 : Oct
    		 : SD-1.5<br>Stability AI
    		 : Nov
    		 : SD2.0<br>Stability AI
    2023 : Jul
    		 : SD-XL<br>Stability AI
    		 : Nov
    		 : SD-Trubo（ADD）<br>Stability AI
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "ICLR 2" : 2
    "NIPS 7" : 7
    "ICML 4" : 4
    "CVPR 1" : 1
```

```mermaid
pie title 单位
    "Machine Learning Group Universiteit van Amsterdam 1" : 1
    "Universite ́ de Montre ́al 1" : 1
    "Stanford University 2" : 2
    "Google DeepMind 2" : 2
    "OpenAI 6" : 6
    "UC Berkeley 1" : 1
    "Tsinghua University 1" : 1
    "Google Brain 2" : 2
    "Ludwig Maximilian University of Munich & Heidelberg University 1" : 1
    "Stability AI 4" : 4
```



# 3. 关联

黄色代表以VAE为基础的无条件生成模型

绿色代表以Diffusion为基础无条件生成

红色代表VAE基础文本指导的图像生成

蓝色代表以Diffusion条件生成，可以根据外部信息引导图像生成

紫色代表以Diffusion引入分类器来引导图像生成

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
DALL-E-->|引入Transformer|CogView
Diffusion_Model-->|逐步优化策略|DDPM
DDPM-->|优化生成时间|DDIM
DDPM-->|优化损失函数<br>优化生成时间|IDDPM
DDIM-->|引入分类器指导训练和生成|ADM
DDPM-->|全方位微调，引入分类器指导训练和生成|ADM
ADM-->|条件分类器改为CLIP|GLIDE
CLIP-->|图文分类器|GLIDE
Classifier-Free_Diffusion-->|无条件分类器工程化实现|GLIDE
DALL-E-->|两阶段训练|DALL-E2
DALL-E2-->|多层级联<br>对比效果<br>优化缺点|Imagen
GLIDE-->|引入CLIP<br>对比结果|DALL-E2
VAE-->|低维隐空间|LDM
DALL-E2-->|在低维空间加噪去噪|LDM
LDM-->|理论基础<br>工程实现<br>预训练好的CLIP来映射关系|Stable_Diffusion
Stable_Diffusion-->|增强数据集清晰和图文理解能力<br>提高生成分辨率|SD1.5
OpenCLIP-->|预训练|SD2.0
SD1.5-->|更高分辨率生成<br>更强的文本语义理解能力|SD2.0
SD2.0-->SDXL
知识蒸馏-->ADD
GAN-->ADD
SDXL-->SD-Turbo
ADD-->|理论基础|SD-Turbo



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
IDDPM[I-DDPM（2021.02）<br>优化了损失函数，让训练更平滑，更能拟合对数似然<br>优化了生成步骤，跳步生成，速度更快]
	style IDDPM fill:#63E398
ADM[DvsG（2021.05）<br>全方位微调DDPM<br>引入分类器指导图像生成，提高精度牺牲多样性<br>性能全面超越GANs]
	style ADM fill:#BA5EB3
CogView[CogView（2021.05）<br>将文本和图像拼接送入潜空间词典一起映射<br>提出大参数Transformer优化训练的模块<br>针对不同下游任务进行微调]
	style CogView fill:#EF7A6D
Classifier-Free_Diffusion[Classifier-Free Diffusion（2022.07）<br>引入无条件分类器指导模型生成]
	style Classifier-Free_Diffusion fill:#BA5EB3
CLIP[CLIP（2021.01）<br>首个将文本指导图像模型学习做到效果不错的]
GLIDE[GLIDE（2021.12）<br>无条件分类器工程化实现<br>基于CLIP的条件分类器<br>BERT的思路实现图像修补]
	style GLIDE fill:#BA5EB3
DALL-E2[DALL·E2（2022.04）<br>引入CLIP将图像提取成embed指导生成过程]
	style DALL-E2 fill:#98CCFF
Imagen[Imagen（2022.05）<br>使用LLM提取文本特征<br>优化生成溢出（-1,1）<br>优化Unet结构<br>多层级联告诉模型添加了多少噪声]
	style Imagen fill:#98CCFF
LDM[LDM（2021.12）<br>在低维空间优化以降低时间复杂度]
	style LDM fill:#98CCFF
Stable_Diffusion[Stable Diffusion（2022.08）]
	style Stable_Diffusion fill:#98CCFF
SD1.5[SD1.5（2022.10）<br>数据集清洗+高分辨率生成（512）]
	style SD1.5 fill:#98CCFF
SD2.0[SD2.0（2022.11）<br>更高分辨率生成（768）]
	style SD2.0 fill:#98CCFF
OpenCLIP[OpenCLIP<br>LAION]
SDXL[SDXL（2023.07）<br>模型更大<br>两个文本编码器<br>能生成更大尺度图像<br>优化训练策略]
style SDXL fill:#98CCFF
ADD[ADD（2023.11）<br>对抗扩散蒸馏，提高扩散模型生成速度]
知识蒸馏[知识蒸馏（2015.03）]
GAN[GAN（2014.06）]
SD-Turbo[SD-Turbo（2023.11）<br>使用ADD加速生成过程]
style SD-Turbo fill:#98CCFF
```





# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [VAE,GAN,DM,V-V,V-V2,I-GPT,DDPM,DDIM,I-DD,D-E1,ADM, CV,GLI,LDM,D-E2,Imag,CFD,SDXL]
    y-axis "Cite" 
    bar [46034, 83283, 8634,6258, 2329, 2050, 23847, 8896,4481,6536, 9492, 911,4128,20780, 8252,6983,4679,2713]
    line [46034, 83283, 8634,6258, 2329, 2050, 23847, 8896,4481,6536, 9492, 911,4128,20780, 8252,6983,4679,2713]
```



