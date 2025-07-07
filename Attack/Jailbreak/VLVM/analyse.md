# 1.年份

取arxiv最早提交时间

```mermaid
timeline
    title Jailbreak_VLVM
    	2023 : Jul
    			 : VAE-JLLM<br>AAAI 2024<br>Princeton University
    			 : Nov
    			 : FigStep<br>AAAI 2025(Oral)<br>Tsinghua University
    			 
    
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "AAAI 2" : 2
```

```mermaid
pie title 单位
    "Princeton University 1" : 1
    "Tsinghua University 1" : 1
```



# 3. 关联

 Vicuna 这种没有微调过安全性的，轻松被突破。相比之下，Llama2 会更保守，SeaLLM-v2 在特定语言上做得最好。



```mermaid
flowchart BT
	VLVM-->Text
	VLVM-->Image
	Hotflip-->|文本攻击方式|VAE-JLLM
	Text-->VAE-JLLM
	Text-->FigStep
	Image-->FigStep
	Image-->VAE-JLLM
	VLVM-->Mix

	
	VAE-JLLM[VAE-JLLM（2023.07）<br>文本+对抗图像=>文本<br>首次针对VLM的图像方面进行攻击<br>也测试了文本的攻击，效果不如图像好]
	FigStep[FigStep（2023.11）<br>危险文本转图像=>文本<br>使用危险文本转图像+无害诱导文本诱导模型完成危险问题完形填空]
```

# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [VAE-JLLM,Fig-Step]
    y-axis "Cite" 
    bar [247,190]
    line [247,190]
```



