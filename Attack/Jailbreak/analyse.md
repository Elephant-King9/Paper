# 1.年份

取arxiv最早提交时间

```mermaid
timeline
    title Jailbreak
    	2020 : Oct
    			 : AutoPrompt<br>University of California
    	2023 : Jul
    			 : VLM-Attack<br>Princeton University<br>AAAI 2024
    			 : GCG<br>Carnegie Mellon University
    			 
    
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "AAAI 1" : 1
```

```mermaid
pie title 单位
    "Carnegie Mellon University 1" : 1
    "University of California 1" : 1
    "Princeton University 1" : 1
```



# 3. 关联

```mermaid
flowchart BT
	Jailbreak-->LLM
	Jailbreak-->VLM
	VLM-->Text
	VLM-->Image
	Hotflip-->|文本攻击方式|VLM-Attack
	Image-->VLM-Attack
	VLM-->Mix
	AutoPrompt-->|提供优化思路|GCG
	LLM-->GCG
	AutoPrompt[AutoPrompt（2020.10）<br>提供了指导模型说出知识的方法]
	GCG[GCG（2023.07）<br>问题后插入对抗句子，引导模型生成Sure+问题]
	VLM-Attack[VLM-Attack（2023.07）<br>首次针对VLM的图像方面进行攻击<br>也测试了文本的攻击，效果不如图像好]
```



# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [AutoPrompt,VLM-Attack,GCG]
    y-axis "Cite" 
    bar [2157, 247, 1631]
    line [2157, 247,1631]
```



