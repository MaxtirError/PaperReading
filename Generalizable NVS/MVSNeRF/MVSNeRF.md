## Task
[[Generalizable NVS]]
## Method
![[Pasted image 20231020190215.png]]
### Warping feature maps
起手还是一个CNN，然后通过一个homographic warping把所有的Feature Map Wrap到参考视角
![[Pasted image 20231020190635.png]]
![[Pasted image 20231020190649.png]]
用的是NDC坐标[[NDC]]
这个Wraping其实可以直接理解为从NDC坐标投影到某个视点下的坐标
### Cost Volume
NDC坐标是扭曲的，大概形状如图a所示，每个Volume $P(u,v,z)$计算cost feature是不同View Wrap过来的方差
![[Pasted image 20231020192617.png]]
注意到这里只有方差，原因是Cost Volume的作用是定几何的，不需要颜色信息。
然后过一个3D Conv，变成$S=B(P)$，其中B代表Conv，也就是做一个Encoding
### NeRF Rendering
就是一个MLP A，表达式是
$$
(RGB\sigma) = A(x,d,f,c)
$$
输出是NeRF渲染常规的输出。
输入的x,d也是常规的。
这里的f是把当前视点下的位置x，反投影到标准NDC空间之后，用encode财产出来的$S$三线性插值得到的特征，表达了这个网络的几何信息
c是投影到各个View下的color的concate
## 论文链接
![[2103.15595.pdf]]