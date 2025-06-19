# 1.年份

取arxiv最新版本提交时间与论文截稿时间之间的较早时间

```mermaid
timeline
    title LLM
    2017 : Jun
    		 : Transformer<br>NIPS 2017
    2018 : Jun
    		 : GPT-1<br>OpenAI
    		 : Oct
    		 : BERT<br>NAACL 2019
    2019 : Feb
    		 : GPT-2<br>OpenAI
    2020 : May
    		 : GPT-3
    2022 : Mar
    		 : InstructGPT<br>OpenAI
```





# 2. 期刊

```mermaid
pie title 期刊类型
		"OpenAI 3" : 3
		"NIPS 2" : 2
		"NAACL 1" : 1
```

# 3. 关联

绿色代表Transformer-Encoder only

黄色代表Transformer-Decoder only

红色代表Transformer-Encoder+Decoder

```mermaid
flowchart BT
Transformer-->|Encoder|BERT
Transformer-->|Decoder|GPT-1
ELMo-->|双向学习思想|BERT
GPT-1-->|扩大数据规模|GPT-2
GPT-2-->|更大的规模|GPT-3
Sparse_Transformer-->|提供Attention改进|GPT-3
GPT-3-->|人工标注优化|InstructGPT




Transformer@{ shape: circle, label: "Transformer（2017.06）" }
				style Transformer fill:#EF7A6D
GPT-1[GPT-1（2018.06）<br>仅使用Decoder<br>当前位置仅知道之前的信息<br>无监督训练+监督微调]
	style GPT-1 fill:#F3D266
BERT[BERT（2018.10）<br>仅使用Encoder<br>当前位置知道前后信息<br>两个句子同时输入<br>同时学习句子是否相邻+预测MASK单词]
	style BERT fill:#63E398
ELMo[ELMo（2018）<br>RNN+双向思想]
GPT-2[GPT-2（2019.02）<br>无监督预训练+Zero-Shot<br>适配下游任务不动模型参数<br>随着模型和训练数据扩大<br>模型还远未达到上限]
	style GPT-2 fill:#F3D266
Sparse_Transformer[Sparse Transformer（2019.04）]
GPT-3[GPT-3（2020.05）<br>更大的无监督预训练<br>完全不需要下游微调就能适配大多数下游任务]
	style GPT-3 fill:#F3D266
InstructGPT[InstructGPT（2022.03）<br>通过人工标注的数据集+新训练的强化训练网络来微调GPT-3]
	style InstructGPT fill:#F3D266
```



# 4. 引用量

```mermaid
    xychart-beta
    title "Cite Num"
    x-axis [Transformer,GPT-1,BERT,GPT-2,GPT-3,InstructGPT]
    y-axis "Cite" 
    bar [185289,13424,133047,16676,48070,15295]
    line [185289,13424,133047,16676,48070,15295]
```



