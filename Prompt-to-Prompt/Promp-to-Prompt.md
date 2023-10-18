## Task
一个Prompt $P$生成了一个图片$I$
给定一个guidance$P^*$  希望Edit图片$I$到$I^*$
Edit的类型如下：
1. Word Swap：更换一个词汇
2. Prompt Refinement：往prompt里面加 tokens
3. Attention Re-weighting：加强或减少某个prompt
## Ideas
生成图片的结构和外观不只由Diffusion Model的随机种子确定，还有Attention Map决定
![[Pasted image 20231018202315.png]]
### Attention Map
Diffusion Model的pipeline：prompt->tokens，然后再某个timesteps下，tokens->key，pixels/features->q，tokens->v，做transform的attention步骤
$$
M=Softmax(\frac{QK^T}{\sqrt d})
$$
M就是所谓Attention Map，$M_{ij}$表示了第i个pixels对第j个tokens的相似度

上图的可视化就是平均了所有timesteps下的tokens，得到的M图片。

额外的结论，这种featuremap 在diffusion的early stage就已经得到

## Method
于是可以把模型看成$DM(z_t,P,t,s)$，有下面的算法
![[Pasted image 20231018202918.png]]
不同任务其实对应着不同的Edit过程
1. Word Swap：设定一个阈值，阈值前用一个Map，阈值后用另一个Map
2. Prompt Refinement：把新的Map中有和旧Map对应关系的，把旧的替换过去
3. Attention Re-weighting：把某个M乘上某个倍数
## 论文链接
![[Prompt-to-Prompt_preprint.pdf]]