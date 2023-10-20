## Task
[[Generalizable NVS]]
从若干个View生成一个Novel View
## Method
![[Pasted image 20231020175924.png]]
大致思路就是把所有的Image 和Pos对输入到一个CNN，输出Patch Embeddings，然后Encode成一个Latent Representation，在Decoder回去，这样就可以使用Transformers的Attention结构了
### CNN
#### Pose information
首先选定一个初始相机，然后把其他相机通过如下公式进行位置编码，连接到图片的颜色通道之后
![[Pasted image 20231020180648.png]]
然后过一个CNN得到$F_i^{CNN}$，还要加一个Position Embedding让每个patch aware位置
![[Pasted image 20231020180738.png]]
然后还要让他区分普通相机和标准相机
![[Pasted image 20231020180914.png]]
最后Flatten成若干个Patch
### Encoder-Deccoder
没有什么特别的的操作，Encoder里面把CNN得到的Patch Embedding做一个Self-Attention得到所谓“Set-Latent Scence Representation”，然后Decoder对每个Ray做一个Cross Attention输出颜色
## 论文链接
![[2111.13152.pdf]]