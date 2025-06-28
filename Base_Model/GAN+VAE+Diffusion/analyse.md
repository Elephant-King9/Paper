# 1.年份

取arxiv上最早的版本

```mermaid
timeline
    title VAE+Diffusion
    2013 : Dec
    		 : VAE<br>ICLR 2014<br>Machine Learning Group Universiteit van Amsterdam

    2014 : Jun
    		 : GAN<br>NIPS 2014<br>Universite ́ de Montre ́al
    2017 : Nov
    		 : VQ-VAE<br>NIPS 2017<br>Google DeepMind
    2019 : VQ-VAE2<br>NIPS 2019<br>Google DeepMind
```





# 2. 期刊

```mermaid
pie title 期刊类型
    "ICLR 1" : 1
    "NIPS 3" : 3
```

# 3. 关联

```mermaid
flowchart BT
VAE-->VQ-VAE
straight-through_estimator-->|离散化梯度传播|VQ-VAE
PixelCNN-->|作为Prior生成器|VQ-VAE
```





# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [VAE,GAN,VQ-VAE,VQ-VAE2]
    y-axis "Cite" 
    bar [46034, 83283, 6258, 2329]
    line [46034, 83283, 6258, 2329]
```



