# 1.年份

取arxiv最新版本提交时间与论文截稿时间之间的较早时间

```mermaid
timeline
    title Image_Restoration
    2018: Jul
    		: RCAN(ECCV2018)
    2021: Aug
    		: SwinIR(ICCV2021)
    		:	Nov
    		: Uformer(CVPR2022)
    2022: Mar
    		: Restormer(CVPR2022)
    		: Apr
    		: ESRT(CVPRW2022)
    		: May
    		: Cat(NIPS2022)
    2023: Feb
    		: ART(ICLR2023)
    		: Mar
    		: HAT(CVPR2023)
  			: Aug
    		: DAT(ICCV2023)
  			: Oct
  			: SRFormer(ICCV2023)
  			: SPIN(ICCV2023)
    2024: Apr
    		: MAN(CVPRW2024)
    		: May
    		: SPAN（CVPRW2024）
    		: Jun
    		: AST(CVPR2024)
    		: Aug
    		: ASID(AAAI2025)
    		: Nov
    		: CATANet(CVPR2025)
    
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "ECCV 1" : 1
    "ICCV 4" : 4
    "CVPR 5" : 5
    "CVPRW 3": 3
    "NIPS 1" : 1
    "ICLR 1" : 1
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

## 3.1 CNN

```mermaid
flowchart BT
图像恢复-->CNN[CNN]
		CNN-->IR[IR]
		CNN-->SR[SR]
		
		
		IR-->|经典深度CNN去噪模型|DnCNN
		DnCNN-->|提出递归网络结构处理图像噪声|RPCNN
		RPCNN-->|提出块递归去噪网络，进一步提升细节恢复|BRDNet
		
		SR-->|首个将深度CNN引用到超分任务|SRCNN
		SRCNN-->|引入残差学习，加深网络|EDSR
		EDSR-->|首次提出RIR+通道注意力（CA）|RCAN
		SR-->VAN
		VAN-->|改进VAN,使用大卷积核+类Transformer结构|MAN
		
		
		
		RCAN@{ shape: circle, label: "RCAN（2018.7）<br>首次RIR+CA" }
				style RCAN fill:#F3D266
		
		SRCNN@{ shape: circle, label: "SRCNN（2014）" }
		DnCNN[DnCNN（2017）]
		RPCNN[RPCNN（2020）]
		BRDNet[BRDNet（2020）]
		EDSR[EDSR（2017）]
    MAN[MAN（2024.4）]
    style MAN fill:#F3D266
		
```

## 3.2 Transformer
```mermaid
flowchart BT
		Transformer[Transformer]
		SSN-->|提供soft k-means超像素算法|SPIN
		Transformer-->窗口注意力
		Transformer-->通道注意力
		
		
		窗口注意力-->|自由变化窗口的形状和大小|聚类窗口
		窗口注意力-->滑动窗口
		RCAN-->|提供RIR|SwinIR
		RCAN-->|提供RIR|ART
		RCAN-->|提供RIR|SRFormer
		窗口注意力-->空洞窗口
		窗口注意力-->大窗口
		窗口注意力-->UNet
		
		滑动窗口-->SwinIR
		空洞窗口-->ART
		大窗口-->SRFormer
		UNet-->|Unet+W-MSA弥补交互问题|UFormer
		聚类窗口-->|没有使用RIR,在窗口的基础上引入聚类,Top-K解决像素数量不一致的问题|SPIN
		
		通道注意力-->|Unet+C-MSA+更新FFN|Restormer
		
		UFormer@{ shape: circle, label: "UFormer（2021.11）<br>首个UNet+Transfomer" }
				style UFormer fill:#63E398
		SwinIR@{ shape: circle, label: "SwinIR（2021.8）<br>首个滑动窗口工作<br>W-MSA+SW-MSA" }
				style SwinIR fill:#EF7A6D
		Restormer@{ shape: circle, label: "Restormer（2022.3）<br>首个C-MSA" }
				style Restormer fill:#63E398
    SPIN@{ shape: circle, label: "SPIN（2023.10）<br>首个聚类窗口" }
    		style SPIN fill:#F3D266
    RCAN@{ shape: circle, label: "RCAN（2018.7）<br>首次RIR+CA" }
				style RCAN fill:#F3D266
    		
    窗口注意力[窗口注意力<br>W-MSA]		
    滑动窗口[滑动窗口<br>SW-MSA]
    
    
   	ART[ART（2023.2）<br>首个空洞窗口工作]
				style ART fill:#EF7A6D
		SRFormer[SRFormer（2023.10）<br>首个大窗口工作<br>改良FFN]
				style SRFormer fill:#F3D266
				
		SSN[SSN（2018）]
```



```mermaid
flowchart BT
		
		SSN-->|提供soft k-means超像素算法|SPIN
		SPIN-->|优化|CATANet
		RCAN-->|提供RIR|CATANet
		RCAN --> |提供RIR网络结构思想|SwinIR
		SwinIR-->|提供W-MSA+SW-MSA|HAT
		RCAN -->|提供RIR+CA|HAT
		HAT-->|提供重叠窗口|CATANet
		
		RCAN-->|提供RIR|Cat
		UFormer-->|Unet|Cat
		SwinIR-->|提供W-MSA+SW-MSA|Cat
		UFormer-->|提供Unet|AST
		SwinIR-->|提供W-MSA+SW-MSA|AST
		
		SwinIR-->|提供W-MSA+C-MSA|DAT
		RCAN-->|提供RIR|DAT
		Restormer-->|提供C-MSA|DAT
		
		UFormer@{ shape: circle, label: "UFormer（2021.11）<br>首个UNet+Transfomer" }
				style UFormer fill:#63E398
		SwinIR@{ shape: circle, label: "SwinIR（2021.8）<br>首个滑动窗口工作<br>W-MSA+SW-MSA" }
				style SwinIR fill:#EF7A6D
		RCAN@{ shape: circle, label: "RCAN（2018.7）<br>首个RIR+CA" }
				style RCAN fill:#F3D266
		Restormer@{ shape: circle, label: "Restormer（2022.3）<br>首个C-MSA" }
				style Restormer fill:#63E398
    SPIN@{ shape: circle, label: "SPIN（2023.10）<br>首个聚类窗口" }
    		style SPIN fill:#F3D266
		
	
		HAT[[HAT（2023.3）<br>首个重叠窗口<br>RIR+W-MSA+SW-MSA+CA+重叠窗口]]
				style HAT fill:#F3D266
		Cat[Cat\Cat_Unet（2022.5）<br>首个长方形注意力<br>SR使用RIR,IR使用Unet<br>W-MSA+SW-MSA+Att\Conv并行]
				style Cat fill:#EF7A6D
		AST[AST（2024.6）<br>W-MSA+SW-MSAA+FRFN<br>Att+FRFN过滤无用信息]
				style AST fill:#63E398
		DAT[DAT（2023.8）<br>RIR+W-MSA+C-MSA+并行卷积+改良FFN]
				style DAT fill:#F3D266
		SSN[SSN（2018）]
		CATANet[CATANet（2024.11）<br>RIR+CATA+IASA+IRCA解决信息丢失问题<br>优化聚类划分，提高单次迭代效率]
			style CATANet fill:#F3D266
		

```
## 3.3 轻量化
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
    x-axis [RCAN,SwinIR,Uformer,Restormer,ESRT,CAT,ART,HAT,DAT,SRFormer,SPIN,MAN,SPAN,AST,ASID,CATANet]
    y-axis "Cite" 
    bar [6048,3133,2016,4123,556,193,135,933,291,224,36,81,36,43,2,1]
    line [6048,3133,2016,4123,556,193,135,933,291,224,36,81,36,43,2,1]
```



# 5. 实验结果

†代表使用Image_Net预训练

DF2K:DIV2K+Filckr2K

[实验结果](./SR_result.xlsx)

# 6. 上采样部分

**==全部采用conv提升通道+PixelShuffle将提升通道扩展到空间==**

效率高、易训练、相比插值算法可学习

Unet结构会使用反卷积来进行层与层的上采样，与这种方式相比又有什么差别？

![image-20250523165743969](/Users/sitianyi/Paper/CV/Super_Resolution(SR)/assets/pics/analyse/image-20250523165743969.png)

对于高分辨率恢复可不可以使用一半反卷积一半conv+PS？



```mermaid
flowchart BT
	RCAN-->|标准+轻量化优化,标准先使用conv改变维度加ReLU后接RCAN的上采样|SwinIR
	RCAN-->|一样|ESRT
	SwinIR-->|直接使用SwinIR的标准|CAT
	SwinIR-->|直接使用SwinIR的标准|ART
	SwinIR-->|直接使用SwinIR的标准|HAT
	SwinIR-->|拓展通道数（96->180）+直接使用使用SwinIR标准+轻量化|DAT
	DAT-->|通道维度保持180，在轻量化基础上减少一层卷积|MAN
	SwinIR-->|直接使用SwinIR标准+轻量化|SRFormer
	RCAN-->|RCAN最后conv前插入ReLU非线性,降低通道（96->40）|SPIN
	SPIN-->|直接使用SPIN|CATANet
	SwinIR-->|直接使用SwinIR轻量化，后接像素裁剪，降低通道（96->64）|ASID
	
	
	
	RCAN[RCAN（2018.7）]
	SwinIR[SwinIR（2021.8）]
	CAT[CAT（2022.5）]
	ART[ART（2023.2）]
	HAT[HAT（2023.3）]
	DAT[DAT（2023.8）]
	SRFormer[SRFormer（2023.10）]
	MAN[MAN（2024.4）]
	SPIN[SPIN（2023.10）]
	CATANet[CATANet（2024.11）]
	ASID[ASID（2024.8）]
	ESRT[ESRT（2022.4）]
	SPAN[SPAN（2024.5）<br>SwinIR轻量化]
```

