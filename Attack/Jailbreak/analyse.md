# 1.年份

取arxiv最早提交时间

```mermaid
timeline
    title Jailbreak
    	2020 : Oct
    			 : AutoPrompt<br>University of California
    	2023 : Jul
    			 : MasterKey<br>NDSS 2024<br>Nanyang Technological University
    			 : VAE-JLLM<br>AAAI 2024<br>Princeton University
    			 : GCG<br>Carnegie Mellon University
    			 : Aug
    			 : CipherChat<br>ICLR 2024<br>The Chinese University of Hong Kong
    			 : Nov
    			 : DeepInception<br>NIPS workshop 2024<br>Hong Kong Baptist University
    			 : FigStep<br>AAAI 2025(Oral)<br>Tsinghua University
    			 
    
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "AAAI 2" : 2
    "NIPS 1" : 1
    "ICLR 1" : 1
    "NIPS workshop 1" : 1
    "NDSS 1" : 1
```

```mermaid
pie title 单位
    "Carnegie Mellon University 1" : 1
    "University of California 1" : 1
    "Princeton University 1" : 1
    "Singapore University of Technology and Design 1 " : 1
    "Tsinghua University 1" : 1
    "The Chinese University of Hong Kong 1" : 1
    "Hong Kong Baptist University 1" : 1
    "Nanyang Technological University 1" : 1
```



# 3. 关联



```mermaid
flowchart BT
	Jailbreak-->LLM
	LLM-->MasterKey
	LLM-->GCG
	LLM-->CipherChat
	Milgram_experiment-->|灵感|DeepInception
	
	GCG-->|对比|DeepInception
	Jailbreak-->VLM
	VLM-->Text
	VLM-->Image
	Hotflip-->|文本攻击方式|VAE-JLLM
	Text-->VAE-JLLM
	Text-->FigStep
	Image-->FigStep
	Image-->VAE-JLLM
	VLM-->Mix
	AutoPrompt-->|提供优化思路|GCG
	
	
	MasterKey[MasterKey（2023.07）<br>探索了LLM是如何检测危险言论的<br>微调LLM让其能生成危险言论的问题]
	DeepInception[DeepInception（2023.11）<br>引诱模型进行角色扮演，多轮对话诱导越狱]
	Milgram_experiment[米尔格拉姆实验（Milgram experiment）<br>它旨在探讨普通人在权威命令下，是否愿意对他人施加痛苦]
	AutoPrompt[AutoPrompt（2020.10）<br>提供了指导模型说出知识的方法]
	GCG[GCG（2023.07）<br>文本+对抗文本=>文本<br>问题后插入对抗句子，引导模型生成Sure+问题]
	VAE-JLLM[VAE-JLLM（2023.07）<br>文本+对抗图像=>文本<br>首次针对VLM的图像方面进行攻击<br>也测试了文本的攻击，效果不如图像好]
	FigStep[FigStep（2023.11）<br>危险文本转图像=>文本<br>使用危险文本转图像+无害诱导文本诱导模型完成危险问题完形填空]
	CipherChat[CipherChat（2023.08）<br>加密文本对话<br>模拟加密文本用正常语言对话]
```



# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [AutoPrompt,MasterKey,AttackVLM,VAE-JLLM,GCG,CipherChat,DeepInception,Fig-Step]
    y-axis "Cite" 
    bar [2157, 212,247, 1631,284,216,190]
    line [2157, 212,247,1631,284,216,190]
```



