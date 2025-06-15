# 1.年份

取arxiv最新版本提交时间与论文截稿时间之间的较早时间

```mermaid
timeline
    title Lightweight_Image_Restoration
    2022: Apr
    		: ESRT<br>CVPRW2022
    2023: LatticeNets<br>TPAMI2023
    2024: Apr
    		: Compacter<br>ACMMM2024
    		: Aug
    		: ASID<br>AAAI2025 
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "CVPRW 1": 1
    "AAAI 1" : 1
    "TPAMI 1" : 1
    "ACMMM 1" : 1
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
		Restormer-->|提供C-MSA|Compacter
		SwinIR-->|提供W-MSA|Compacter
		SwinIR-->|提供W-MSA|ASID
		SwinIR-->|提供W-MSA|ESRT
		RCAN-->|提供CA|ESRT
		LatticeNet-->|1.引入模块泛化<br>2.引入对比损失优化性能<br>3.细节与可视化分析拓展<br>4.更全面的实验验证|LatticeNets
		
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
			
		LatticeNet[LatticeNet<br>ECCV2020]
		LatticeNets[LatticeNets<br>TPAMI2023<br>CNN网络优化残差链接<br>引入对比学习损失指导训练]
			style LatticeNets fill:#EF7A6D
		Compacter[Compacter（2024.4）<br>C-MSA+W-MSA+共享QKV<br>L1损失+频域损失]
			style Compacter fill:#EF7A6D
```

**==1. 所有Transformer SR工作都在RIR结构上进行（SPIN）==**

**==2. 所有Transformer IR工作全在U-Net上进行==**

# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [ESRT,ASID,LatticeNets,Compacter]
    y-axis "Cite" 
    bar [556,2,67,0]
    line [556,2,67,0]
```



# 5. 实验结果

†代表使用Image_Net预训练

DF2K:DIV2K+Filckr2K

BSD-gray:BSDS500的会不版本

噪声图像通过在干净图像上添加 **加性白高斯噪声（AWGN）** 

## 5.1 Mult-Add和FLOPs的关系

![image-20250615173102624](./assets/pics/analyse/image-20250615173102624.png)

[实验结果](/assests/IR_SR_Lightweight_Result.xlsx)