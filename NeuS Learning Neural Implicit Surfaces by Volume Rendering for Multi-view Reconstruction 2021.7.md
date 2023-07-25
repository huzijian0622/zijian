## NeuS: Learning Neural Implicit Surfaces by Volume Rendering for Multi-view Reconstruction 2021.7

![image-20230725091032833](/Users/huzijian/Library/Application Support/typora-user-images/image-20230725091032833.png)

 提出了一种将nerf用于三维重建领域的方法；相较于传统表面重建 ， nerf的优势在于根据图片的rgb可以很好重建出物体的深度信息；

但nerf作为一种体渲染的方法，关注的重点在于颜色的渲染，在纹理的渲染上存在模糊的现象，并且由于在图片中会存在颗粒灰尘，所以nerf体渲染的结果往往带有杂质点。

文章提出了利用sdf与nerf结合的方法，这可以解决：

（1）无偏

（2）自遮挡问题

​    其中sdf是一种隐式函数来重建三维表面；不同于显式，sdf作为一种符号距离函数，表示一种离表面的距离场，可以实现三维到一维的映射：
$$
R^3\rightarrow R
$$
  

nerf的公式可以总结为：
$$
C(o,v)=\int_{1}^{\infty}\omega(t)c(p(t),v)dt
$$




<img src="/Users/huzijian/Library/Application Support/typora-user-images/image-20230725091909395.png" alt="image-20230725091909395" style="zoom:50%;" />



其中无偏代表在物体的表面，渲染出来的颜色应该为最大值；

自遮挡则代表在同一条射线上，当和两个重建表面接触时，离观测点近的位置颜色值应当比远的大。

<img src="/Users/huzijian/Library/Application Support/typora-user-images/image-20230725093337164.png" alt="image-20230725093337164" style="zoom:50%;" />

重建效果：

![image-20230725101059091](/Users/huzijian/Library/Application Support/typora-user-images/image-20230725101059091.png)



缺点：重建的时间提高。



### Geo-Neus: Geometry-Consistent Neural Implicit Surfaces Learning for Multi-view Reconstruction 2022.5

<img src="/Users/huzijian/Library/Application Support/typora-user-images/image-20230725103004460.png" alt="image-20230725103004460" style="zoom:50%;" />

**1.sdf loss**

首先需要找到隐式表面，即
$$
\partial\Omega={p|sdf(p)=0}
$$
所以需要找到点集合：
$$
T=\lbrace t|sdf(t_i)\cdot sdf(t_{i+1})<0 \rbrace
$$
根据点集合内插出表面点集合。



**2.利用了MVS对sdf做约束**

参考mvsnet，利用单适应变换矩阵，构造几何一致性损失函数

**3.体渲染颜色约束**

nerf的渲染公式













