# 1.年份

取arxiv最新版本提交时间与论文截稿时间之间的较早时间

```mermaid
timeline
    title Backdoor_Diffusion
    2023 : Mar
    		 : TIME<br>ICCV 2023<br>Technion
    2024 : Jul
    		 : EvilEdit<br>ACMMM2024<br>CQU
```





# 2. 期刊

```mermaid
pie title 期刊类型
	"ACMMM 1" : 1
	"ICCV 1" : 1
```

```mermaid
pie title 单位
	"CQU 1" : 1
	"Technion 1" : 1
```



# 3. 关联

```mermaid
flowchart BT
	9-->|图像特征转文本特征|EvilEdit
	TIME-->|理论基础|EvilEdit


	TIME[TIME（2023.03）<br>通过修改注意力矩阵消除Diffusion偏见]
	EvilEdit[EvilEdit（2024.07）<br>通过修改注意力矩阵达到无需训练就能植入后门的方法<br>提供白名单防止原始数据污染]
```
# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [TIME,EvilEdit]
    y-axis "Cite" 
    bar [116,20]
    line [116,20]
```



