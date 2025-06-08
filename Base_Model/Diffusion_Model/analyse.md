# 1.年份

```mermaid
timeline
    title Diffusion_Model
    2022 : Nov
    		 : TrojDiff
    		 : BadDiffusion
    2023 : Mon
    		 : AdvDM
    		 : Apr
    		 : BadT2I
    		 : Aug
    		 : Glaze
    2025 : Apr
    		 : Survey
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "TMLR 1" : 1
```

# 3. 关联



```mermaid
flowchart BT
		Diffusion攻击-->DDPM
		Diffusion攻击-->StableDiffusion
		DDPM-->|首批DDPM后门攻击|TrojDiff
		DDPM-->|首批DDPM后门攻击|BadDiffusion
		StableDiffusion-->|首批SD后门攻击|BadT2I
		Diffusion攻击[Diffusion攻击]
		TrojDiff[TrojDiff（2022.11.11）]
		BadDiffusion[BadDiffusin（2022.11.11）]
		BadT2I[BadT2I（2023.4.12）]
		Glaze[Glaze（2023.8.27）]
		AdvDM[AdvDM（2023.1.31）]
		DDPM[DDPM（2020）]
		StableDiffusion[Stable Diffusion（2021）]
```

# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [survey]
    y-axis "Cite" 
    bar [5]
    line [5]
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

