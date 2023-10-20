OpenGL中的坐标变换如下：
![[Pasted image 20231020195525.png]]
世界坐标就是把物体坐标做平移旋转缩放变成和世界对其的，用的Model Matrix
之后View transformation就是把世界坐标变换到某个Camera视点下的坐标
投影变换到Clip Space，是一个中间状态，坐标参数中有n和f，决定了视点的远近。
最后用透视除法（非线性），转换成NDC坐标，大概就是一个$[-1,1]^3$，里面是n到f的视锥空间
![[Pasted image 20231020195828.png]]