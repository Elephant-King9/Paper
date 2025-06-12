# 1.年份

取arxiv最新版本提交时间与论文截稿时间之间的较早时间

```mermaid
timeline
    title Lightweight_Image_Restoration
    2022: Apr
    		: ESRT<br>CVPRW2022
    2024: Aug
    		: ASID<br>AAAI2025 
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "CVPRW 1": 1
    "AAAI 1" : 1
```

# 3. 关联

- CA:RCAN提出，通道注意力(CNN)
- RIR:RCAN提出，残差中的残差
- C-MSA:Restormer提出通道注意力(Transformer)
- W-MSA:窗口自注意力
- SW-MSA:shift窗口自注意力

---

黄色：超分网络(SR)

绿色：恢复网络(IR)

红色：超分+恢复网络(SR+IR)

----

圆形：关键论文

双括号：值得阅读

```mermaid
flowchart BT
		
		Restormer-->|提供C-MSA|ASID
		SwinIR-->|提供W-MSA|ASID
		SwinIR-->|提供W-MSA|ESRT
		RCAN-->|提供CA|ESRT
		
		SwinIR@{ shape: circle, label: "SwinIR（2021.8）<br>首个滑动窗口工作<br>W-MSA+SW-MSA" }
				style SwinIR fill:#EF7A6D
		Restormer@{ shape: circle, label: "Restormer（2022.3）<br>首个C-MSA" }
				style Restormer fill:#63E398
    
    RCAN@{ shape: circle, label: "RCAN（2018.7）<br>首个RIR+CA" }
				style RCAN fill:#F3D266
    		
    ESRT[ESRT（2022.4）<br>通道减半+共享参数+CA+局部窗口]
				style ESRT fill:#F3D266
		ASID[ASID（2024.8）<br>C-MSA+W-MSA+通道蒸馏+共享A矩阵]
			style ASID fill:#F3D266
			
		SPIN[SPIN（2024.5）<br>CNN+非线性<br>非线性指导特征图更新]
			style SPIN fill:#F3D266
```

**==1. 所有Transformer SR工作都在RIR结构上进行（SPIN）==**

**==2. 所有Transformer IR工作全在U-Net上进行==**

# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [ESRT,ASID]
    y-axis "Cite" 
    bar [556,2]
    line [556,2]
```



# 5. 实验结果

†代表使用Image_Net预训练

DF2K:DIV2K+Filckr2K

[实验结果](./SR_result.xlsx)