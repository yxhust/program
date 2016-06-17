# 3D Scene Reconstruction and Rendering from Multiple Images


## Team

 易旭  贺鹏飞

## Introduction

3D reconstruction from multiple images is the creation of three-dimensional models from a set of images. It is the reverse process of obtaining 2D images from 3D scenes.
The essence of an image is a projection from a 3D scene onto a 2D plane,during which process the depth is lost. The 3D point corresponding to a specific image point is constrained to be on the line of sight. From a single image, it is impossible to determine which point on this line corresponds to the image point. If two images are available, then the position of a 3D point
can be found as the intersection of the two projection rays. This process is referred to as triangulation. The key for this process is the relations between multiple views which convey the information that corresponding sets of points must contain some structure and that this structure is related to the poses and the calibration of the camera.

Please refer to the following videos to better under what is 3D scene reconstruction:

https://www.youtube.com/watch?v=LrvPhSASBjk (YouTube video)

https://www.youtube.com/watch?v=sz0UbHvEttI&index=3&list=PL949A9422C7FB609F (YouTube video)

https://www.youtube.com/watch?v=jtyXkuNPpIg&index=5&list=PL949A9422C7FB609F (YouTube video)

https://www.youtube.com/watch?v=ZEztAxeNQRI&index=6&list=PL949A9422C7FB609F (YouTube video)


## Reference
1. Multi-camera scene reconstruction via graph cuts, In ECCV 2002.
2. Scene Reconstruction and Visualization from Internet Photo Collections,
PhD Thesis, 2008.
3. https://graphics.stanford.edu/~mdfisher/SceneReconstruction.html.


## Time Line
1. 2016-05-19 建立github网站.
2. 2015-05-26 阅读参考文献.
3. 2015-06-02确定重建场景的目标，并找到方法。

## Reference Reading

在《Multi-camera scene reconstruction via graph cuts》一文中，一个经典的问题：如何从任意场景的一系列已知视点图中计算出其三维形状呢？多相机场景重建能很好地解决上述问题，其核心就在于通过图割使能量最小化。首先，我们给出多相机场景重建的能量最小化公式，而最小化的能量能对称地输入图像、合理的处理可视性、保持空间连续性。但是，能量最小化是NP级别难题，而利用图割算法来计算局部的最小化能更好的解决这个问题，最终的实验结果表明方法确实有效。

在《Scene Reconstruction and Visualization from Internet Photo Collections》一文中，使用的源就是互联网中数以万计的图片（不同时间、不同地点、不同天气这些图片的集合）。作者提出一个问题,如何利用这些图片来创造我们这个世界的3D图形界面？要解决这个问题，有两个难题必须要考虑到。第一，要重新构造出图片集中的3D场景必须知道所用的图片的拍摄地点，作者提出了一种新的计算机视觉技术来解决这一问题而不需要借助GPS或其他设备，该方法的关键就在于选取小部分图像做预处理。第二，如何构建这些重建图形界面，以及如何提供有效的场景可视化。为了完成这一目的，作者提出两个全新的3D用户界面，其一是Photo Tourism，这个是能提供图片间进行几何操作的3D图片浏览器，放大、缩小、挑选等等；其二是Pathfinder，其原理利用的是人们更倾向于在名胜古迹拍照，因此Pathfinder能通过分析照片得知所在的位置进而获取导航控件，而这些控件能很轻松的找到每个图片场景的重要部分。
解决了以上两个问题，利用这些技术可以构建系统能够对名胜古迹的3D场景自动构造，用户只需要输入简单的输入几个关键词，系统就会自动的系在图片、重建、获取导航控件，最后提供改良的界面。

## 2016.5.26--2016.6.2
本周首先是通过自由门翻墙软件看YOUTUBE视频，了解场景重建，毕竟场景重建可用在很多方面，为后面具体的做准备。经过一段时间的学习，对Matthew Fisher的Scene Reconstruction有一定的了解，下面对Scene Reconstruction进行介绍：
文中试验、作比较的数据源都是来自 Multi-View Stereo Dataset，而这个数据集是场景重建的标准数据集，而作者采用的两个标准测试集是 the Temple and Dino scenes。那些输入的图片规格都是640x480，并与Yasutaka Furukawa's method（目前最好的算法）的进行比较。
实验主要有以下几步：

1.Image Calibration，图像校准，输入的是一系列图片，输出的相机位置、方位以及固有参数。

2.Depth Map Construction，深度图重建，输入的是一系列上述校准后的图片，输出的图片中每个像素到物体的距离。

3.Mesh Reconstruction，网格重建，输入的一系列校准图与深度图，输出得到的是物体的网格。

4.Texture Generation，纹理生成，输入的是校准图以及物体的网格，输出得到的是一系列图册和纹理。

基于上述的思路，作者提出一种方法,具体步骤如下：

1.Assume calibrated images (all standard scene reconstruction datasets are calibrated)

2.Construct initial depth map guesses

3.Until reconstructed mesh does not change:

--Refine all depth maps

--nstruct mesh from depth maps

--oject reconstructed mesh back into images as new depth maps

4.Simplify and smooth mesh

5.Texture mesh

其中，用到了一个函数Photometric Consistency Function，该函数描述如下：
Given a point x in space and two calibrated images, define a function p(x) between 0 and 1 that is large if x is close to the final surface，也就是说给定空间的一个点以及两个校准图，定义函数p(x）。
按照上述的流程步骤，一步步走下去，最终得到实验结果。
该方法的CPU耗用极低，用GPU非常迅速，Furukawa用了10小时进行全程测试，而此方法生成网格只需15分钟。


##2016.6.3--2016.6.12

经过阅读文献，并在网上查找资料，最终我们组的重建方案是，利用双目视觉图片（网上下载）进行3D场景重建，图像源为一张图的双目图，简单的话可以理解为左右试图，下面一步步从最终结果介绍重建思路以及过程。
1.平台工具
电脑采用win7 64操作系统，工具为VS2012,另外使用OPENCV计算机视觉库以及OPENGL图形程序接口，工作界面如下图所示。
![图片工作界面](https://github.com/yxhust/program/blob/master/工作界面.png)

2.计算特征匹配
对于双目图片，在真实世界中为同一张图，找出对应点，运用OPENCV里面的库算法来完成，结果如下图。
![图片1](https://github.com/yxhust/program/blob/master/1.png)

3.计算三维坐标
上面找到了匹配点，接下来需要计算真实世界中图片的3D坐标，用到的是投影原理，结果如下图。
![图片2](https://github.com/yxhust/program/blob/master/2.png)

4.三角剖分
将双目视图中的一张进行三角剖分，得到很多三角块，用于最终的立体场景重建，三角剖分结果如下图。
![图片3](https://github.com/yxhust/program/blob/master/3.jpg)

5.3D重建
前面的准备工作就绪之后，最终利用OPENGL里面的函数进行纹理贴图得到重建结果图，如下所示
![图片4](https://github.com/yxhust/program/blob/master/4.png)



##2016.6.13--2016.6.18
上周已经完成了主要工作，本周就是对代码进行整理确保不出错。
另外完成readme的编写，以及最后一次课上的presentation ppt和demo的制作。

成员分工如下：

贺鹏飞—特征点匹配、计算三维坐标

易旭—三角剖分、3D重建


代码连接如下：
链接: http://pan.baidu.com/s/1gfoEooz 密码: 7xuv








## To Do List
1. Read papers.
2. Do some experiments.
3. Use Matthew Fisher's method to complete scene reconstruction.
