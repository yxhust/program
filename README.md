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

## Reference Reading

在《Multi-camera scene reconstruction via graph cuts》一文中，一个经典的问题：如何从任意场景的一系列已知视点图中计算出其三维形状呢？多相机场景重建能很好地解决上述问题，其核心就在于通过图割使能量最小化。首先，我们给出多相机场景重建的能量最小化公式，而最小化的能量能对称地输入图像、合理的处理可视性、保持空间连续性。但是，能量最小化是NP级别难题，而利用图割算法来计算局部的最小化能更好的解决这个问题，最终的实验结果表明方法确实有效。

在《Scene Reconstruction and Visualization from Internet Photo Collections》一文中，使用的源就是互联网中数以万计的图片（不同时间、不同地点、不同天气这些图片的集合）。作者提出一个问题,如何利用这些图片来创造我们这个世界的3D图形界面？要解决这个问题，有两个难题必须要考虑到。第一，要重新构造出图片集中的3D场景必须知道所用的图片的拍摄地点，作者提出了一种新的计算机视觉技术来解决这一问题而不需要借助GPS或其他设备，该方法的关键就在于选取小部分图像做预处理。第二，如何构建这些重建图形界面，以及如何提供有效的场景可视化。为了完成这一目的，作者提出两个全新的3D用户界面，其一是Photo Tourism，这个是能提供图片间进行几何操作的3D图片浏览器，放大、缩小、挑选等等；其二是Pathfinder，其原理利用的是人们更倾向于在名胜古迹拍照，因此Pathfinder能通过分析照片得知所在的位置进而获取导航控件，而这些控件能很轻松的找到每个图片场景的重要部分。
解决了以上两个问题，利用这些技术可以构建系统能够对名胜古迹的3D场景自动构造，用户只需要输入简单的输入几个关键词，系统就会自动的系在图片、重建、获取导航控件，最后提供改良的界面。


## To Do List
1. Read papers.
2. Do some experiments.
