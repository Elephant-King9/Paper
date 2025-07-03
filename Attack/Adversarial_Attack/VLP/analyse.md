# 1.年份

```mermaid
timeline
    title VLP_Adv_Attack
    2022← : Sep_Attack
    2022 : Jun
    		 : Co-Attack<br>ACMMM 2022<br>Beijing Jiaotong University
    2023 : May
    		 : AttackVLM<br>NIPS 2023<br>Singapore University of Technology and Design
    		 : Jul
    		 : SGA<br>ICCV 2023<br>Southern University of Science and Technology
    2024 : TMM
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "ICCV 1" : 1
    "ACM MM 1" : 1
    "S&P 1" : 1
    "NIPS 1" : 1
```

```mermaid
pie title 期刊类型
 "Beijing Jiaotong University 1" : 1
 "Singapore University of Technology and Design 1" : 1
 "Southern University of Science and Technology 1" : 1
```



# 3. 关联



```mermaid
flowchart BT
    FGSM-->|图像攻击|Co-Attack
    BERT-Attack-->|文本攻击|Co-Attack
    Co-Attack-->|将单一图文对扩展到图文对集合|SGA
	  RGF-->|黑盒梯度优化方式|AttackVLM
	  
	  
	  Co-Attack[Co-Attack（2022.06）<br>提出了模态混合攻击<br>图像使用FGSM优化混合模态<br>文本使用BERT-Attack优化混合模态<br>分析了单模态下文本图像的攻击效果，以及单双流模型的鲁棒性]
	  AttackVLM[AttackVLM（2023.05）<br>提出了针对Caption任务的攻击方法，通过对图像添加扰动来让VLM生成不匹配图像的描述]
	  FGSM[FGSM]
	  RGF[RGF（2015.11）<br>研究了不用梯度信息怎么优化一个目标函数]
	  SGA[SGA（2023.07）<br>将跨模态攻击由单一文本对扩展到集合提升鲁棒性<br>通过最大化余弦相似度优化<br>干净图像=>扰动文本1=>扰动图像=>扰动文本2]
```

# 4. 引用量

```mermaid

    xychart-beta
    title "Cite Num"
    x-axis [Co-Attack, AttackVLM,SGA, TMM]
    y-axis "Cite" 
    bar [115, 270,69,32]
    line [115, 270,69,32]
```

# 5. 汇总

```mermaid
mindmap
  root((VLP_Adv_Attack))
    Sep-Attack
      Co-Attack
      	SGA
       TMM
    
```

