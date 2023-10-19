## Task
[[Diffusion-Based 2D Image Editing]]
输入一张图片$I^G$和Prompt$P$作为Guidance，生成一张图片服从$P$并保持$I^G$的结构和语义布局

## Ideas
考虑Stable Diffusion的一个Unet Layers
![[Pasted image 20231019135149.png]]
这篇文章的Key Observation是：
1. Unet Decoder 结构编码了局部语义信息，并且较少被外观影响。
2. self-attention可以保留精细的布局和形状细节

### Decoder Layers
证明第一点，做了如下两个实验
![[Pasted image 20231019135545.png]]
第一个实验是把不同Layers在某个timesteps用PCA把三个最主要的成分抓出来，然后可视化
认为第四层代表的就是全局语义信息，越深表达的信息越高频。
![[Pasted image 20231019135826.png]]
第二个实验是证明上述现象在所有的timesteps都是一致的
### Self-Attention
![[Pasted image 20231019135917.png]]
证明第二点也是同理，把Self-Attention可视化出来，发现Self-Attention控制的就是局部语义信息
## Method
基于上述两点，在算法中设计Feature Injection和Attention Injection即可
![[Pasted image 20231019140029.png]]
## 论文链接
![[2211.12572.pdf]]