## Tasks
[[Generalizable NVS]]
从single view或者少量的View 去生成一个3D表达
## Method
### Single View
![[Pasted image 20231019202510.png]]
1. 对于Input View$I$，首先过一个CNN把它Encode成$W=E(I)$
2. 对于给定的一个Ray上的某个点$x$，把它反投影到Input View上，然后通过bilinear插值成$W(\pi (x))$
3. 把这些信息塞到一个NeRF中，也就是$f(\gamma(x), d, W(\pi (x)))=(RGB\sigma)$
5. 做Volum Rendering就行
## Multi View
魔改一下$f=f_2 \cdot f_1$
$f_1$就是之前的$f$，$f_2$对每个View过$f_1$后的结果做一个池化
## 论文链接
![[2012.02190.pdf]]