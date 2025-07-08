# 1.年份

取arxiv最早提交时间

```mermaid
timeline
    title Jailbreak_VLVM
    	2023 : Jul
    			 : VAE-JLLM<br>AAAI 2024<br>Princeton University
    			 : Nov
    			 : FigStep<br>AAAI 2025(Oral)<br>Tsinghua University
    			 : QR<br>ECCV 2024<br>Shanghai AI Laboratory
    	2024 : May
    			 : VRP<br>arxiv<br>University of Wisconsin–Madison
 
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "AAAI 2" : 2
    "arxiv 1" : 1
    "ECCV 1" : 1
```

```mermaid
pie title 单位
    "Princeton University 1" : 1
    "Tsinghua University 1" : 1
    "University of Wisconsin–Madison 1" : 1
    "Shanghai AI Laboratory 1" : 1
```



# 3. 关联

 Vicuna 这种没有微调过安全性的，轻松被突破。相比之下，Llama2 会更保守，SeaLLM-v2 在特定语言上做得最好。



```mermaid
flowchart BT
	VLVM-->文本+对抗图像
	VLVM-->文本_图像
	Hotflip-->|文本攻击方式|VAE-JLLM
	文本+对抗图像-->VAE-JLLM
	文本_图像-->FigStep
	文本_图像-->QR
	QR-->|将图像从物体改为角色<br>并增加角色描述|VRP
	
	
	
	
	文本+对抗图像[文本+对抗图像]
	文本_图像[文本=>图像]
	VAE-JLLM[VAE-JLLM（2023.07）<br>文本+对抗图像=>文本<br>首次针对VLM的图像方面进行攻击<br>也测试了文本的攻击，效果不如图像好]
	FigStep[FigStep（2023.11）<br>危险问题=>图像+完形填空<br>使用危险文本转图像+无害诱导文本诱导模型完成危险问题完形填空]
	VRP[VRP（2024.05）<br>危险问题=>危险角色+角色描述+危险问题<br>找到了通用的坏人角色]
	QR[QR（2023.11）<br>危险问题=>危险文本对应的图像+危险问题<br>构建了多模态数据集<br>使用文本帮助防御]
```

# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [VAE-JLLM,Fig-Step, QR, VRP]
    y-axis "Cite" 
    bar [247,190,140,35]
    line [247,190,140,35]
```



