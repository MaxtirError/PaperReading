## Task
[[Diffusion Tunning-Free Editing]]
给定一张Guidance图片，比如是从某个图片上画一些草图或者是笔画作为guidance，要生成一张真实图片
## Method
把这张图片Denoised到$t_0$ Steps，然后用Diffusion Model Denoised
### 如何选取t
实际上是真实性和忠实度的trade-off
采用KID [[Kernel Inception Score]]衡量图片是否真实
使用生成的图片与原图的 L2范数衡量图片是否忠于guidance
在两者较小的t区间选取
### 理论证明
证明了如果想要生成真实的图片，必须牺牲一部分的忠实度【定量解释上面的Trade-off】
## 原论文链接
![[2108.01073.pdf]]