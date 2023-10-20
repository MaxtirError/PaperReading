## Task
[[Generalizable NVS]]
## Method
![[Pasted image 20231020213812.png]]
整体的框架非常清晰，就在底下的说明里面。
1. 过CNN提Feature，然后先过一个Cross-View Transformer
2. Volume render的一个点先逆映射回所有View得到Feature，然后两两计算cos相似度，和位置方向拼接起来得到最后的c和$\sigma$，$\sigma$用一个Transformer做Self Attention
### Cross-View Transformer
用GMFlow[[GMFlow]]中定制的Transformers