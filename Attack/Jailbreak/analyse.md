# 1.年份

取arxiv最早提交时间

```mermaid
timeline
    title Jailbreak
    	2020 : Oct
    			 : AutoPrompt<br>University of California
    	2023 : Jul
    			 : VAE-JLLM<br>AAAI 2024<br>Princeton University
    			 : GCG<br>Carnegie Mellon University
    			 : Nov
    			 : FigStep<br>AAAI 2025(Oral)<br>Tsinghua University
    			 
    
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "AAAI 2" : 2
    "NIPS 1" : 1
```

```mermaid
pie title 单位
    "Carnegie Mellon University 1" : 1
    "University of California 1" : 1
    "Princeton University 1" : 1
    "Singapore University of Technology and Design 1 " : 1
    "Tsinghua University 1" : 1
```



# 3. 关联



```mermaid
flowchart BT
	Jailbreak-->LLM
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
	LLM-->GCG
	AutoPrompt[AutoPrompt（2020.10）<br>提供了指导模型说出知识的方法]
	GCG[GCG（2023.07）<br>文本+对抗文本=>文本<br>问题后插入对抗句子，引导模型生成Sure+问题]
	VAE-JLLM[VAE-JLLM（2023.07）<br>文本+对抗图像=>文本<br>首次针对VLM的图像方面进行攻击<br>也测试了文本的攻击，效果不如图像好]
	FigStep[FigStep（2023.11）<br>危险文本转图像=>文本<br>使用危险文本转图像+无害诱导文本诱导模型完成危险问题完形填空]
```



# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [AutoPrompt,AttackVLM,VAE-JLLM,GCG,Fig-Step]
    y-axis "Cite" 
    bar [2157, 270,247, 1631,190]
    line [2157, 270,247,1631,190]
```



