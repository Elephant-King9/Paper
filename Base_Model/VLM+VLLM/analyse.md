# 1.年份

取arxiv最新版本提交时间与论文截稿时间之间的较早时间

```mermaid
timeline
    title VLM+MLLM
    2021 : Jan
    		 : CLIP<br>ICML 2021
    		 : ViLT<br>ICML 2021
    		 : May
    		 : ALBEF<br>NIPS 2021 
    2022 : Jan
    		 : BLIP<br>ICML 2022
    		 : May
    		 : VLMo<br>NIPS 2022
    		 : Jun
    		 : CoCa<br>Google
    		 : Aug
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



视觉编码器应该大于文本编码器

融合模块很重要

对比学习ITC Loss很好(ITC(Iamge-Text-Contrastive))

目标检测WPA Loss算起来很慢(WPA（Word Patch Alignment）)

BERT的Mask Loss不错 [Mask Language Modling]

Image Text Matching Loss不错

所以好的Loss=ITC+ITM+MLM

```mermaid
flowchart BT
	Transformer-->CLIP
	Visual_N-Grams-->CLIP
	VirTex-->CLIP
	ICMLM-->CLIP
	ConVIRT-->|简化+学习对比学习|CLIP
	Transformer-->ViLT
	Transformer-->ALBEF
	Transformer-->VLMo
	
	Transformer-->BLIP
	Transformer-->CoCa
	Transformer-->BEiT_v3
	Transformer-->PaLI
	
	
	
	Transformer[Transformer]
		style Transformer fill:#EF7A6D
	ViLT[ViLT]
		style ViLT fill:#F3D266
	CLIP[CLIP（2021.01）<br>首个将文本指导图像模型学习做到效果不错的<br>引入对比学习<br>实现Zero-Shot高性能]
		style CLIP fill:#F3D266
	ALBEF[ALBEF]
		style ALBEF fill:#F3D266
	VLMo[VLMo]
		style VLMo fill:#F3D266
	BLIP[BLIP]
		style BLIP fill:#EF7A6D
	CoCa[CoCa]
		style CoCa fill:#EF7A6D
	BEiT_v3[BEiT v3]
		style BEiT_v3 fill:#EF7A6D
	PaLI[PaLI]
		style PaLI fill:#EF7A6D
	VirTex[VirTex（2020）<br>1. 对图像I生成描述文本T<br>2. 用交叉熵损失来生成文本和原始文本对齐]
	ICMLM[ICMLM（2020）<br>使用Masked Language Modeling（MLM）训练图文模型<br>模仿BERT]
	ConVIRT[ConVIRT（2020）<br>医学图文<br>使用对比学习]
	Visual_N-Grams[Visual N-Grams（2017）<br>首个尝试用图文对齐做零样本分类]
```



# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [CLIP, ViLT, ALBEF, BLIP,VLMo,Coca,BEiT v3,PaLI]
    y-axis "Cite" 
    bar [36752,2115,2412,5442,623,1710,660,794]
    line [36752,2115,2412,5442,623,1710,660,794]
```



