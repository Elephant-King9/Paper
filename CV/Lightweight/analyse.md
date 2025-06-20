# 1.年份

取arxiv最新版本提交时间与论文截稿时间之间的较早时间

```mermaid
timeline
    title Lightweight_Image_Restoration
    2022: Apr
    		: ESRT<br>CVPRW2022
    		: Jun
    		: HNCT<br>CVPRW2022
    2023: LatticeNets<br>TPAMI2023
    		: Jun
    		: STSN<br>CVPRW2023
    2024: Apr
    		: Compacter<br>ACMMM2024
    		: RAMiT<br>CVPRW2024
    		: Mar
    		: LIDFormer<br>AAAI2024
    		: Jul
    		: SRConvNet<br>IJCV2025
    		: Aug
    		: ASID<br>AAAI2025 
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "CVPRW 4": 4
    "AAAI 2" : 2
    "TPAMI 1" : 1
    "ACMMM 1" : 1
    "IJCV 1" : 1
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
		Restormer-->|提供C-MSA|RAMiT
		MobileNetV2-->|改进模块MobiVari|RAMiT
		SwinIR-->|提供W-MSA|RAMiT
		SwinIR-->|提供W-MSA|Compacter
		SwinIR-->|提供W-MSA|ASID
		SwinIR-->|提供W-MSA|ESRT
		SwinIR-->|提供W-MSA|SRConvNet
		频域-->SRConvNet
		RCAN-->|提供CA|ESRT
		SwinIR-->|提供W-MSA|HNCT
		RFA-->|提供模块ESA|HNCT
		RFA-->|提供模块ESA|STSN
		LatticeNet-->|1.引入模块泛化<br>2.引入对比损失优化性能<br>3.细节与可视化分析拓展<br>4.更全面的实验验证|LatticeNets
		
		SwinIR@{ shape: circle, label: "SwinIR（2021.8）<br>首个滑动窗口工作<br>W-MSA+SW-MSA" }
				style SwinIR fill:#EF7A6D
		Restormer@{ shape: circle, label: "Restormer（2022.3）<br>首个C-MSA" }
				style Restormer fill:#63E398
    
    RCAN@{ shape: circle, label: "RCAN（2018.7）<br>首个RIR+CA" }
				style RCAN fill:#F3D266
		频域@{ shape: circle, label: "频域" }
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
		RAMiT[RAMiT（2024.4）<br>C-MSA+W-MSA，每个C-MSA与前一个W-MSA融合，反之亦然<br>加入MobiVari]
			style RAMiT fill:#EF7A6D
		MobileNetV2[MobileNetV2（CVPR2018）]
		RFA[RFA（CVPR2020）]
		STSN[STSN（2023.6）<br>CNN+ESA]
			style STSN fill:#F3D266
		HNCT[HNCT（2022.6）<br>S-MSA+ESA]
			style HNCT fill:#F3D266
		SRConvNet[SRConvNet（2024.7）<br>S-MSA+频域+组动态卷积]
			style SRConvNet fill:#EF7A6D
```

# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [ESRT,HNCT,ASID,LatticeNets,STSN,RAMiT,LIDFormer,SRConvNet,Compacter]
    y-axis "Cite" 
    bar [556,196,2,67,26,16,8,11,0]
    line [556,196,2,67,26,16,8,11,0]
```



# 5. 实验结果

†代表使用Image_Net预训练

DF2K:DIV2K+Filckr2K

BSD-gray:BSDS500的会不版本

噪声图像通过在干净图像上添加 **加性白高斯噪声（AWGN）** 

## 5.1 Mult-Add和FLOPs的关系

![image-20250615173102624](./assets/pics/analyse/image-20250615173102624.png)

![image-20250616203115446](./assets/pics/analyse/image-20250616203115446.png)

[实验结果](/assests/IR_SR_Lightweight_Result.xlsx)