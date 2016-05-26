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

在《Scene Reconstruction and Visualization from Internet Photo Collections》一文中，


## To Do List
1. Read papers.
