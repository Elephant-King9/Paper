# 1.年份

取arxiv最新版本提交时间与论文截稿时间之间的较早时间

```mermaid
timeline
    title Conv
    2024 : Nov
    		 : FD-Conv<br>CVPR2025

```





# 2. 期刊

```mermaid
pie title 期刊类型
    "CVPR 1" : 1
```

# 3. 关联

```mermaid
flowchart BT
		
		Conv-->动态卷积
		动态卷积-->CondConv-->DYConv-->ODConv-->FDConv
		
		
		
		动态卷积[动态卷积<br>根据输入动态调整卷积权重]
		Conv[Conv]
		CondConv[Cond-Conv<br>使用Sigmoid加权]
		DYConv[DY-Conv<br>改进为使用softmax<br>加权更稳定]
		ODConv[OD-Conv<br>进一步将注意力细化为<br>通道维 卷积核维 空间维<br><b>参数量增加<b>]
		FDConv[FD-conv<br>CVPR2025<br>从频域重建]
```



# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [FD-Conv]
    y-axis "Cite" 
    bar [0]
    line [0]
```



