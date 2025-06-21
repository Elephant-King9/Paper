# 1.年份

取arxiv最新版本提交时间与论文截稿时间之间的较早时间

```mermaid
timeline
    title VLM+MLLM
    2021 : Jan
    		 : CLIP<br>ICML 2021<br>OpenAI
    		 : ViLT<br>ICML 2021<br>Kakao
    		 : May
    		 : ALBEF<br>NIPS 2021<br>Salesforce
    		 : Jun
    		 : BEiT<br>Microsoft
    		 : Aug
    		 : SimVLM<br>ICLR 2022<br>Google
    		 : Nov
    		 : VLMo<br>NIPS 2022<br>Microsoft
    2022 : Jan
    		 : BLIP<br>ICML 2022<br>Salesforce
    		 : May
    		 : Jun
    		 : CoCa<br>Google
    		 : Aug
    		 : BEiT v2<br>
    		 : BEiT v3<br>CVPR 2023
    		 : Oct
    		 : PaLI<br>ICLR 2023
```





# 2. 期刊

```mermaid
pie title 期刊类型
		"NIPS 2" : 2
		"ICML 3" : 3
		"CVPR 1" : 1
		"ICLR 1" : 1
```

# 3. 关联

绿色代表Transformer-Encoder only

黄色代表Transformer-Decoder only

红色代表Transformer-Encoder+Decoder



- 单流架构
  - 图像和文本的嵌入 在输入阶段就拼接（concatenate）在一起，然后统一送入同一个 Transformer 中处理
  - 优点
    - 模态间融合充分、交互层次深
    - 结构简洁（只有一个Transformer Encoder）
  - 缺点
    - 文本图像的token共享Attention空间，可能会相互干扰
    - 对内存和计算的要求高
- 双流架构
  - 图像和文本分别用 两个独立的 Transformer 编码器处理，直到某一层才进行交互（比如通过 Cross Attention）
  - 优点
    - 模态内部的建模更纯净，不容易干扰。
    - 更易调控图像和文本的参数配比。
  - 缺点
    - 模型更复杂，**参数量更大**。
    - 模态间交互较晚，可能错失早期融合的效果。

视觉编码器应该大于文本编码器

融合模块很重要

对比学习ITC Loss很好(ITC(Iamge-Text-Contrastive))

目标检测WPA Loss算起来很慢(WPA（Word Patch Alignment）)

BERT的Mask Loss不错 [Mask Language Modling]

Image Text Matching Loss不错

所以好的Loss=ITC+ITM+MLM

```mermaid
flowchart BT
	subgraph 视觉使用目标检测_淘汰
		direction BT
		目标检测-->Region_Feature_1
    Region_Feature_1-->UNITER
    Region_Feature_1-->ViLBERT
	end
	Region_Feature-->|使用图像增强|ViLT
	Visual_N-Grams-->CLIP
	VirTex-->CLIP
	ICMLM-->CLIP
	ConVIRT-->|简化+借鉴对比学习|CLIP
	MoCo-->|提供图像对比学习思路|ALBEF
	Knowledge_Distillation-->|知识蒸馏思想|ALBEF
	CLIP-->|ITC时利用CLIP|VLMo
	CLIP-->|对比学习|ALBEF
	ViLT-->|图像数据增强|ALBEF
	ALBEF-->|ITM困难负样本挖掘|VLMo
	VLMo-->|根据下游任务动态调整模块|BLIP
	ALBEF-->|ITC+ITM训练逻辑<br>优化数据集过滤|BLIP
	GPT-1-->|Deocder LM训练逻辑|BLIP
	SimVLM-->BLIP
	ALBEF-->|网络结构|CoCa
	BLIP-->|Decoder|CoCa
	
	
	
	

	目标检测[目标检测<br>使用预训练好的目标检测模型来提取特征<br>视觉预训练模型无法学习]
	ViLT[ViLT（2021.01）<br>单流架构,轻量化<br>整词遮蔽+图像增强<br>摒弃目标检测<br>ViT处理图像<br>ITM+MLM+WPA]
		style ViLT fill:#63E398
	CLIP[CLIP（2021.01）<br>图像处理=文本处理<br>特征简单融合（点乘）<br>首个将文本指导图像模型学习做到效果不错的<br>引入对比学习<br>实现Zero-Shot高性能<br>ITC]
		style CLIP fill:#63E398
	ALBEF[ALBEF（2021.05）<br>双流架构<br>摒弃目标检测<br>ITM+MLM+ITC<br>引入蒸馏和MoCo图像对比学习]
		style ALBEF fill:#63E398
	VLMo[VLMo（2021.11）<br>单双流融合<br>针对不同下游任务切换单双<br>图像+文本+混合分别训练<br>三个FFN<br>ITC:CLIP<br>MLM:BERT<br>ITM:ALBEF]
		style VLMo fill:#63E398
	BLIP[BLIP（2022.01）<br>Encoder+Decoder<br>根据下游任务不同切换不同模块<br>过滤加字幕生成过滤数据集]
		style BLIP fill:#EF7A6D
	CoCa[CoCa（2022.06）<br>ALBEF网络架构<br>将Text Encoder替换为Decoder<br>图像模态引入Attention Pooling<br>ITC+LM]
		style CoCa fill:#EF7A6D
	BEiT_v3[BEiT v3]
		style BEiT_v3 fill:#EF7A6D
	PaLI[PaLI]
		style PaLI fill:#EF7A6D
	VirTex[VirTex（2020）<br>1. 对图像I生成描述文本T<br>2. 用交叉熵损失来生成文本和原始文本对齐]
	ICMLM[ICMLM（2020）<br>使用Masked Language Modeling（MLM）训练图文模型<br>模仿BERT]
	ConVIRT[ConVIRT（2020）<br>医学图文<br>使用对比学习]
	Visual_N-Grams[Visual N-Grams（2017）<br>首个尝试用图文对齐做零样本分类]
	Region_Feature[Region Feature（2018）<br>首次提出Region Feature<br>在图像中提取主体区域<br>图像数据增强]
	Region_Feature_1[Region Feature（2018）<br>首次提出Region Feature<br>在图像中提取主体区域<br>图像数据增强]
	UNITER[UNITER<br>单流架构]
	ViLBERT[ViLBERT<br>双流架构]
	MoCo[MoCo<br>通过动量+队列构造字典来对比学习<br>让数据集在没有标注的情况下还能让视觉模型学到较好的表征能力]
	Knowledge_Distillation[Knowledge_Distillation（2015）<br>知识蒸馏]
	GPT-1[GPT-1（2018.06）<br>仅使用Decoder<br>当前位置仅知道之前的信息<br>无监督训练+监督微调]
		style GPT-1 fill:#F3D266
	SimVLM[SimVLM<br>首个Decoder生成模型]
		style SimVLM fill:#EF7A6D
```



```mermaid
flowchart BT

	PixelBERT[PixelBERT（2020）<br>不使用目标检测器<br>直接使用ResNet提取图像特征<br>更简单，但精细对齐略弱]
	VSE++[VSE++（2017）<br>模态不对等<br>图像处理>文本处理<br>相似度简单融合（点乘）]
	SCAN[SCAN（2017）<br>模态不对等<br>图像处理>文本处理<br>相似度简单融合（点乘）]
	UNITER[UNITER（2019）<br>模态不对等<br>图像处理>文本处理<br>模态间复杂融合]
	VL-BERT[VL-BERT（2019）<br>模态不对等<br>图像处理>文本处理<br>模态间复杂融合]
	VisualBERT[VisualBERT<br>单流架构]
	UNITER[UNITER<br>单流架构]
	ViLBERT[ViLBERT<br>双流架构]
	LXMERT[LXMERT<br>双流架构]
```



# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [CLIP, ViLT, ALBEF, VLMo, BLIP,Coca,BEiT v3,PaLI]
    y-axis "Cite" 
    bar [36752,2115,2412,623,5442,1710,660,794]
    line [36752,2115,2412,623,5442,1710,660,794]
```



