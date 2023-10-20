## Task
[[Diffusion Tunning-Free Editing]]
和P2P是完全一样的任务[[Promp-to-Prompt]]
就是给定一张图片，和一个新的Prompt，然后把一张图片Edit到另一张图片
## Ideas
1. 图片的布局在Diffusion的早期就形成了
2. 图片的语义内容蕴藏在Self-Attention的Query Features
第一点其实和很多文章是类似的，因此主要关注第二点。
![[Pasted image 20231019153145.png]]
看到，两张不同的马的图片，在Query Feature上的颜色是相似的。所以这篇文章就着手在了Self-Attention的改动上
## Method
![[Pasted image 20231019153315.png]]
根据上面的分析，实际上关键就是Edit的设计。

### Mutual Self-Attention

![[Pasted image 20231019153405.png]]
如图，实际上就是把Sourcec的K和V抓过来，Target只保留Q，formulation就是
![[Pasted image 20231019153437.png]]
这里个人的理解是相当于把Self-Attention变成了一个Cross-Attention。只不过这个Cross-Attention不是多模态的，而是Source和Dst之间的。如果Query，Key，Value中都是某种语义布局信息，那么可以理解为，用Query保Target的语义布局，然后去”询问“Source，Target的语义布局对应Source的语义布局的哪些部分，从而实现了Source到Target的外观上的保留，语义上的迁移。
所以后面的Mask-Guided也很好理解。就是把这种Guidance分成前景和背景。相当于人为地先将背景的语义分割，再去寻找对应。
![[Pasted image 20231019154032.png]]
## 论文链接
![[2304.08465.pdf]]