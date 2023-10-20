## Tasks
[[Generalizable NVS]]
给定若干个View，生成一个Novel View
## Method
基本的方法和[[pixelNerf]]很像，就是对于Target View 的一条Ray，Sample若干个点，把这若干个点逆映射回Source View，然后提Feature过网络，不过网络结构有不少Tricky的部分。下面是整体的架构
![[Pasted image 20231020132056.png]]
![[Pasted image 20231020132037.png]]
### 提取Feature
首先是为了结合Local和Global的信息，对于N个Views，提取出所有View的信息之后它把所有Feature取Mean和方差得到$\mu,v$，concate起来得到最终的feature去过MLP
### 池化过程
Feature过MLP之后生成了新的Feature和一个权重，池化使用的是加权平均和方差再映射到最终的$f_\sigma$ 表示density的feature。
权重的生成方式如下：
![[Pasted image 20231020133259.png]]
s是一个可学习的参数。目的是为了减少最远图片的影响。
我的理解是，如果一张图片和Target View Wrap的太厉害，那么这张图片的feature就不太作数，这个式子相当于是对$d\cdot d_i$ 用exp做一个放大，也就是离得越远的图片这个weight越小，这有就可以排除掉远处图片的影响
### Ray Transformer
简单来说就是沿着Ray做一个Self-Attention去计算density
## 论文链接
![[2102.13090.pdf]]