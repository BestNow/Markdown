# 7  Viewing 视图

In the previous chapter, we saw how to use matrix transformations as a tool for arranging geometric objects in 2D or 3D space. A second important use of geometric transformations is in moving objects between their 3D locations and their positions in a 2D view of the 3D world. This 3D to 2D mapping is called a viewing transformation, and it plays an important role in object-order rendering, in which we need to rapidly find the image-space location of each object in the scene. 
在前一章中，我们了解了如何利用矩阵变换作为在二维或三维空间中排列几何对象的工具。几何变换的第二个重要应用是在将物体从其三维位置移动到它们在三维世界的二维视图中。这种从三维到二维的映射被称为视图变换，它在对象顺序渲染中扮演着重要的角色，因为我们需要快速找到场景中每个物体在图像空间中的位置。

When we studied ray tracing in Chapter 4, we covered the different types of perspective and orthographic views and how to generate viewing rays according to any given view. This chapter is about the inverse of that process. Here we explain how to use matrix transformations to express any parallel or perspective view. The transformations in this chapter project 3D points in the scene (world space) to 2D points in the image (image space), and they will project any point on a given pixel’s viewing ray back to that pixel’s position in image space. 
当我们在第 4 章中学习光线追踪时，我们介绍了不同类型的透视和正交视图以及如何根据任何给定视图生成观察光线。 本章讨论的是该过程的逆过程。 在这里，我们解释如何使用矩阵变换来表达任何平行视图或透视图。 本章中的变换将场景（世界空间）中的 3D 点投影到图像（图像空间）中的 2D 点，并且它们会将给定像素的视线上的任何点投影回该像素在图像空间中的位置。

If you have not looked at it recently, it is advisable to review the discussion of perspective and ray generation in Chapter 4 before reading this chapter. 
如果你最近没有看过它，建议在阅读本章之前回顾一下第 4 章中关于透视和光线生成的讨论。

By itself, the ability to project points from the world to the image is only good for producing wireframe renderings—renderings in which only the edges of objects are drawn, and closer surfaces do not occlude more distant surfaces (Figure 7.1). Just as a ray tracer needs to find the closest surface intersection along each viewing ray, an object-order renderer displaying solid-looking objects has to work out which of the (possibly many) surfaces drawn at any given point on the screen is closest and display only that one. In this chapter, we assume we are drawing a model consisting only of 3D line segments that are specified by the $(x, y, z)$ coordinates of their two endpoints. Later chapters will discuss the machinery needed to produce renderings of solid surfaces. 
就其本身而言，将点从世界投影到图像的能力仅适用于生成线框渲染，即仅绘制对象边缘的渲染，并且较近的表面不会遮挡较远的表面（图 7.1）。 正如光线追踪器需要沿着每条观察光线找到最近的表面交点一样，显示实体外观对象的对象顺序渲染器也必须计算出在屏幕上的任何给定点绘制的哪个（可能是多个）表面最接近，并且 只显示那个。 在本章中，我们假设我们正在绘制一个仅由 3D 线段组成的模型，这些线段由其两个端点的 $(x, y, z)$ 坐标指定。 后面的章节将讨论生成实体表面渲染所需的机械。
<img src=".\Images\Figure 7.1.png" alt="Figure 7.1" style="zoom:67%;" />
Figure 7.1. Left: wireframe cube in orthographic projection. Middle: wireframe cube in perspective projection. Right: perspective projection with hidden lines removed. 
图 7.1.  左：正交投影中的线框立方体。 中：透视投影中的线框立方体。 右：删除隐藏线的透视投影。



## 7.1 Viewing Transformations 视图变换

The viewing transformation has the job of mapping 3D locations, represented as $(x, y, z)$ coordinates in the canonical coordinate system, to coordinates in the image, expressed in units of pixels. It is a complicated beast that depends on  many different things, including the camera position and orientation, the type of projection, the field of view, and the resolution of the image. As with all complicated transformations it is best approached by breaking it up into a product of several simpler transformations. Most graphics systems do this by using a sequence of three transformations: 
视图变换的任务是将 3D 位置（在规范坐标系中表示为 $(x, y, z)$ 坐标）映射到图像中的坐标（以像素为单位表示）。 它是一个复杂的野兽，取决于许多不同的因素，包括相机的位置和方向、投影类型、视野和图像的分辨率。 与所有复杂的转换一样，最好的方法是将其分解为几个更简单的转换的产物。 大多数图形系统通过使用三个转换序列来实现此目的：

> Some APIs use “viewing transformation” for just the piece of our viewing transformation that we call the camera transformation. 
> 一些 API 将“视图变换”仅用于我们称为相机变换的视图变换部分。

- A camera transformation or eye transformation, which is a rigid body transformation that places the camera at the origin in a convenient orientation. It depends only on the position and orientation, or pose, of the camera.
  相机变换或眼睛变换，这是一种刚体变换，它将相机以方便的方向放置在原点。 它仅取决于相机的位置和方向或姿势。
- A projection transformation, which projects points from camera space so that all visible points fall in the range -1 to 1 in x and y. It depends only on the type of projection desired.
  投影变换，从相机空间投影点，以便所有可见点都落在 x 和 y 的 -1 到 1 范围内。 这仅取决于所需的投影类型。
- A viewport transformation or windowing transformation, which maps this unit image rectangle to the desired rectangle in pixel coordinates. It depends only on the size and position of the output image. 
  视口变换或窗口变换，将单位图像矩形映射到像素坐标中所需的矩形。 它仅取决于输出图像的大小和位置。

To make it easy to describe the stages of the process (Figure 7.2), we give names to the coordinate systems that are the inputs and output of these transformations.  The camera transformation converts points in canonical coordinates (or world space) to camera coordinates or places them in camera space. The projection transformation moves points from camera space to the canonical view volume.  Finally, the viewport transformation maps the canonical view volume to screen space. 
为了便于描述该过程的各个阶段（图 7.2），我们为作为这些变换的输入和输出的坐标系命名。 相机变换将规范坐标（或世界空间）中的点转换为相机坐标或将它们放置在相机空间中。 投影变换将点从相机空间移动到规范视图体积。 最后，视口变换将规范视图体积映射到屏幕空间。
<img src=".\Images\Figure 7.2.png" alt="Figure 7.2" style="zoom:67%;" />

Figure 7.2. The sequence of spaces and transformations that gets objects from their original coordinates into screen space. 
图 7.2. 将对象从原始坐标转换到屏幕空间的空间和变换序列。

> Other names: camera space is also “eye space” and the camera transformation is sometimes the “viewing transformation;” the canonical view volume is also “clip space” or “normalized device coordinates;” screen space is also “pixel coordinates.” 
> 其他名称：相机空间也是“眼睛空间”，相机变换有时是“观看变换”； 规范视图体积也是“剪辑空间”或“标准化设备坐标”； 屏幕空间也是“像素坐标”。

Each of these transformations is individually quite simple. We’ll discuss them in detail for the orthographic case beginning with the viewport transformation, then cover the changes required to support perspective projection.
这些转换中的每一个都非常简单。 我们将从视口转换开始详细讨论正交案例，然后介绍支持透视投影所需的更改。

### 7.1.1 The Viewport Transformation 视口变换

We begin with a problem whose solution will be reused for any viewing condition. We assume that the geometry we want to view is in the canonical view volume,  and we wish to view it with an orthographic camera looking in the $-z$ direction. The canonical view volume is the cube containing all 3D points whose Cartesian coordinates are between $-1$ and $+1$—that is, $(x, y, z) ∈ [-1, 1]^3$ (Figure 7.3) We project $x = -1$ to the left side of the screen, $x = +1$ to the right side of the screen, $y = -1$ to the bottom of the screen, and $y = +1$ to the top of the screen. 
我们从一个问题开始，其解决方案将在任何观看条件下重复使用。 我们假设我们想要查看的几何图形位于规范视图体积中，并且我们希望使用正交相机在 $-z$ 方向上查看它。 规范视图体积是包含笛卡尔坐标在 $-1$ 和 $+1$ 之间的所有 3D 点的立方体，即 $(x, y, z) ∈ [-1, 1]^3$（图 7.3 ）我们将 $x = -1$ 投影到屏幕左侧，$x = +1$ 投影到屏幕右侧，$y = -1$ 投影到屏幕底部，$y = +1 $ 到屏幕顶部。
![Figure 7.3](.\Images\Figure 7.3.png)
Figure 7.3. The canonical view volume is a cube with side of length two centered at the origin. 
图 7.3. 规范视图体积是一个边长为 2、以原点为中心的立方体。

> The word “canonical” crops up again—it means something arbitrarily chosen for convenience. For instance, the unit circle could be called the “canonical circle.”
> “规范”这个词再次出现——它的意思是为了方便而任意选择的东西。 例如，单位圆可以称为“规范圆”。

Recall the conventionsfor pixel coordinates from Chapter 3: each pixel “owns” a unit square centered at integer coordinates; the image boundaries have a half-unit overshoot from the pixel centers; and the smallest pixel center coordinates are $(0, 0)$. If we are drawing into an image (or window on the screen) that has $n_x$ by $n_y$ pixels, we need to map the square $[−1, 1]^2$ to the rectangle $[−0.5, n_x − 0.5] × [−0.5, n_y − 0.5]$.
回想一下第 3 章中像素坐标的约定：每个像素“拥有”一个以整数坐标为中心的单位正方形； 图像边界与像素中心有半个单位的超调； 最小像素中心坐标为$(0, 0)$。 如果我们要绘制具有 $n_x$ x $n_y$ 像素的图像（或屏幕上的窗口），我们需要将正方形 $[−1, 1]^2$ 映射到矩形 $[−0.5, n_x − 0.5] × [−0.5, n_y − 0.5]$。

> Mapping a square to a potentially non-square rectangle is not a problem; x and y just end up with different scale factors going from canonical to pixel coordinates.
> 将正方形映射到潜在的非正方形矩形不是问题； x 和 y 最终会得到从规范坐标到像素坐标的不同比例因子。

For now, we will assume that all line segments to be drawn are completely inside the canonical view volume. Later we will relax that assumption when we discuss clipping.
现在，我们假设所有要绘制的线段都完全位于规范视图体积内。 稍后，当我们讨论裁剪时，我们将放宽这一假设。

Since the viewport transformation maps one axis-aligned rectangle to another, it is a case of the windowing transform given by Equation (6.6):
由于视口变换将一个轴对齐的矩形映射到另一个轴对齐的矩形，因此它是等式（6.6）给出的窗口变换的一种情况：
$$
\begin{bmatrix}
x_{screen} \\
y_{screen} \\
1
\end{bmatrix} 
= \begin{bmatrix}
\frac{n_x}{2} & 0 & \frac{n_x - 1}{2} \\
0 & \frac{n_y}{2} & \frac{n_y - 1}{2} \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x_{canonical} \\
y_{canonical} \\
1
\end{bmatrix} \ \ \ \ \ (7.1)
$$
Note that this matrix ignores the z-coordinate of the points in the canonical view volume, because a point’s distance along the projection direction doesn’t affect where that point projects in the image. But before we officially call this the viewport matrix, we add a row and column to carry along the z-coordinate without changing it. We don’t need it in this chapter, but eventually we will need the z values because they can be used to make closer surfaces hide more distant surfaces (see Section 8.2.3).
请注意，该矩阵忽略了规范视图体积中点的 z 坐标，因为点沿投影方向的距离不会影响该点在图像中的投影位置。 但在我们正式将其称为视口矩阵之前，我们添加一行和一列来携带 z 坐标而不更改它。 在本章中我们不需要它，但最终我们将需要 z 值，因为它们可以用来使更近的曲面隐藏更远的曲面（参见第 8.2.3 节）。
$$
M_{vp} = \begin{bmatrix}
\frac{n_x}{2} & 0 & 0 & \frac{n_x - 1}{2} \\
0 & \frac{n_y}{2} & 0 & \frac{n_y - 1}{2} \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix} \ \ \ \ \ \ (7.2)
$$

### 7.1.2 The Orthographic Projection Transformation正交投影变换

Of course, we usually want to render geometry in some region of space other than the canonical view volume. Our first step in generalizing the view will keep the view direction and orientation fixed looking along -z with +y up, but will allow arbitrary rectangles to be viewed. Rather than replacing the viewport matrix, we’ll augment it by multiplying it with another matrix on the right. 
当然，我们通常希望在规范视图体积之外的某些空间区域中渲染几何图形。 我们概括视图的第一步将保持视图方向和方向固定，沿着 -z 和 +y 向上看，但允许查看任意矩形。 我们不是替换视口矩阵，而是通过将其与右侧的另一个矩阵相乘来增强它。

Under these constraints, the view volume is an axis-aligned box, and we’ll name the coordinates of its sides so that the view volume is $[l, r] × [b, t] × [f, n]$ shown in Figure 7.4. We call this box the orthographic view volume and refer to the bounding planes as follows:
在这些约束下，视图体积是一个轴对齐的盒子，我们将命名其边的坐标，以便视图体积为 $[l, r] × [b, t] × [f, n]$ 所示 如图 7.4 所示。 我们将此框称为正交视图体积，并按如下方式引用边界平面： 
![Figure 7.4](.\Images\Figure 7.4.png)
Figure 7.4. The orthographic view volume.
图 7.4. 正交视图体积。
$$
x = l ≡ left\ plane, \\
x = r ≡ right\ plane, \\
y = b ≡ bottom\ plane, \\
y = t ≡ top\ plane, \\
z = n ≡ near\ plane, \\
z = f ≡ far\ plane. \\
$$
That vocabulary assumes a viewer who is looking along the minus z-axis with  his head pointing in the y-direction(Most programmers find it intuitive to have the x-axis pointing right and the y-axis pointing up. In
a right-handed coordinate system, this implies that we are looking in the -z direction. Some systems use a left-handed coordinate system for viewing so that the gaze direction is along +z. Which is best is a matter of taste, and this text assumes a right-handed coordinate system. A reference that argues for the left-handed system instead is given in the notes at the end of the chapter.  ). This implies that $n > f$, which may be unintuitive, but if you assume the entire orthographic view volume has negative $z$ values then the $z = n$ “near” plane is closer to the viewer if and only if $n > f$; here $f$ is a smaller number than $n$, i.e., a negative number of larger absolute value than $n$. 
该词汇假设观看者沿着负 z 轴观看，头指向 y 方向（大多数程序员认为 x 轴指向右侧，y 轴指向上方是直观的。右手坐标系，这意味着我们正在朝 -z 方向看。 一些系统使用左手坐标系进行观察，以便注视方向沿着+z。 哪个最好取决于个人喜好，本文假设使用右手坐标系。 本章末尾的注释中给出了支持左手系统的参考文献。 ）。 这意味着 $n > f$，这可能不直观，但如果假设整个正交视图体积具有负 $z$ 值，则 $z = n$ “近”平面更接近观察者当且仅当 $ n > f$; 这里$f$是比$n$小的数，即绝对值比$n$大的负数。

This concept is shown in Figure 7.5. The transform from orthographic view volume to the canonical view volume is another windowing transform, so we can simply substitute the bounds of the orthographic and canonical view volumes into Equation (6.7) to obtain the matrix for this transformation:
这个概念如图 7.5 所示。 从正交视图体积到规范视图体积的变换是另一种加窗变换，因此我们可以简单地将正交视图体积和规范视图体积的边界代入方程（6.7）以获得该变换的矩阵：
$$
\bold{M}_{orth} = \begin{bmatrix}
\frac{2}{r - l} & 0 & 0 & -\frac{r + l}{r - l} \\
0 & \frac{2}{t - b} & 0 & -\frac{t+b}{t-b} \\
0 & 0 & \frac{2}{n-f} & -\frac{n+f}{n-f} \\
0 & 0 & 0 & 1
\end{bmatrix} \ \ \ \ (7.3)
$$

> This matrix is very close to the one used traditionally in OpenGL, except that $n$, $f$, and $z_{canonical}$ all have the opposite sign.
> 该矩阵与 OpenGL 中传统使用的矩阵非常接近，只是 $n$、$f$ 和 $z_{canonical}$ 都具有相反的符号。

![Figure 7.5](.\Images\Figure 7.5.png)
Figure 7.5. The orthographic view volume is along the negative z-axis, so $f$ is a more negative number than $n$, thus $n > f$. 
图 7.5. 正交视图体积沿着负 z 轴，因此 $f$ 是比 $n$ 更负的数，因此 $n > f$。

To draw 3D line segments in the orthographic view volume, we project them into screen x- and y-coordinates and ignore z-coordinates. We do this by combining Equations (7.2) and (7.3). Note that in a program we multiply the matrices together to form one matrix and then manipulate points as follows:
为了在正交视图体积中绘制 3D 线段，我们将它们投影到屏幕 x 和 y 坐标并忽略 z 坐标。 我们通过结合方程（7.2）和（7.3）来做到这一点。 请注意，在程序中，我们将矩阵相乘以形成一个矩阵，然后按如下方式操作点：
$$
\begin{bmatrix}
x_{pixel} \\
y_{pixel} \\
z_{canonical} \\
1
\end{bmatrix}
=(\bold{M}_{vp}\bold{M}_{orth})\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix}
$$
The z-coordinate will now be in [-1, 1]. We don’t take advantage of this now, but it will be useful when we examine z-buffer algorithms. 
z 坐标现在位于 [-1, 1] 中。 我们现在不利用这一点，但当我们检查 z 缓冲区算法时它会很有用。

The code to draw many 3D lines with endpoints $\bold{a}_i$ and $\bold{b}_i$ thus becomes both simple and efficient: 
因此，绘制许多带有端点 $\bold{a}_i$ 和 $\bold{b}_i$ 的 3D 线的代码变得既简单又高效：
<img src=".\Images\Figure 7.5_1.png" alt="Figure 7.5_1" style="zoom:67%;" />

> This is a first example of how matrix transformation machinery makes graphics programs clean and efficient.
> 这是矩阵变换机制如何使图形程序变得干净和高效的第一个例子。

### 7.1.3 The Camera Transformation  相机转换

We’d like to be able to change the viewpoint in 3D and look in any direction. There are a multitude of conventions for specifying viewer position and orientation. We will use the following one (see Figure 7.6):
我们希望能够改变 3D 视角并朝任意方向观看。 有多种用于指定观看者位置和方向的约定。 我们将使用以下一个（见图 7.6）：
<img src=".\Images\Figure 7.6.png" alt="Figure 7.6" style="zoom:80%;" />
Figure 7.6. The user specifies viewing as an eye position $\bold{e}$, a gaze direction $\bold{g}$, and an up vector $\bold{t}$. We construct a right-handed basis with $\bold{w}$ pointing opposite to the gaze and $\bold{v}$ being in the same plane as $\bold{g}$ and $\bold{t}$.
图 7.6. 用户将观看指定为眼睛位置 $\bold{e}$、注视方向 $\bold{g}$ 和向上向量 $\bold{t}$。 我们构造一个右手基础，其中 $\bold{w}$ 指向凝视方向，并且 $\bold{v}$ 与 $\bold{g}$ 和 $\bold{t}$ 在同一平面上。

- the eye position $\bold{e}$,
  眼睛位置$\bold{e}$,
- the gaze direction $\bold{g}$,
  凝视方向$\bold{g}$,
- the view-up vector $\bold{t}$. 
  视图向上向量$\bold{t}$。

The eye position is a location that the eye “sees from.” If you think of graphics as a photographic process, it is the center of the lens. The gaze direction is any vector in the direction that the viewer is looking. The view-up vector is any vector in the plane that both bisects the viewer’s head into right and left halves and points “to the sky” for a person standing on the ground. These vectors provide us with enough information to set up a coordinate system with origin $\bold{e}$ and a $\bold{uvw}$ basis, using the construction of Section 2.4.7:
眼睛位置是眼睛“观看”的位置。 如果您将图形视为摄影过程，那么它就是镜头的中心。 注视方向是观察者注视方向上的任意向量。 视图向上向量是平面中的任何向量，它将观看者的头部平分为左右两半，并且对于站在地面上的人来说指向“天空”。 这些向量为我们提供了足够的信息来建立一个以原点 $\bold{e}$ 和 $\bold{uvw}$ 为基础的坐标系，使用第 2.4.7 节的构造：
$$
\bold{w} = -\frac{\bold{g}}{\|\bold{g}\|}, \\
\bold{u} = \frac{\bold{t}\cross \bold{w}}{\|\bold{t}\cross \bold{w}\|} \\
\bold{v} = \bold{w} \cross \bold{u}
$$
Our job would be done if all points we wished to transform were stored in coordinates with origin $\bold{e}$ and basis vectors $\bold{u}$, $\bold{v}$, and $\bold{w}$. But as shown in Figure 7.7, the coordinates of the model are stored in terms of the canonical (or world) origin o and the x-, y-, and z-axes. To use the machinery we have already developed, we just need to convert the coordinates of the line segment endpoints we wish to draw from xyz-coordinates into uvw-coordinates. This kind of transformation was discussed in Section 6.5, and the matrix that enacts this transformation is the canonical-to-basis matrix of the camera’s coordinate frame:
如果我们希望变换的所有点都存储在具有原点 $\bold{e}$ 和基向量 $\bold{u}$、$\bold{v}$ 和 $\bold{w}$ 的坐标中，我们的工作就完成了。 但如图 7.7 所示，模型的坐标是根据规范（或世界）原点 o 以及 x、y 和 z 轴存储的。 要使用我们已经开发的机制，我们只需要将要绘制的线段端点的坐标从 xyz 坐标转换为 uvw 坐标。 这种变换在 6.5 节中讨论过，执行这种变换的矩阵是相机坐标系的规范基矩阵：
$$
\bold{M}_{cam} = \begin{bmatrix}
\bold{u} & \bold{v} & \bold{w} & \bold{e} \\
0 & 0 & 0 & 1
\end{bmatrix}^{-1}
= \begin{bmatrix}
x_u & y_u & z_u & 0 \\
x_v & y_v & z_v & 0 \\
x_w & y_w & z_w & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 & −x_e \\
0 & 1 & 0 & −y_e \\
0 & 0 & 1 & −z_e \\
0 & 0 & 0 & 1
\end{bmatrix} \ \ \ \ \ (7.4)
$$
<img src=".\Images\Figure 7.7.png" alt="Figure 7.7" style="zoom:67%;" />
Figure 7.7. For arbitrary viewing, we need to change the points to be stored in the “appropriate” coordinate system. In this case it has origin e and offset coordinates in terms of $\bold{u}\bold{v}\bold{w}$.
图 7.7. 为了任意查看，我们需要更改要存储在“适当”坐标系中的点。 在这种情况下，它具有原点 e 和以 $\bold{u}\bold{v}\bold{w}$ 表示的偏移坐标。

Alternatively, we can think of this same transformation as first moving $\bold{e}$ to the origin, then aligning $\bold{u}$, $\bold{v}$, $\bold{w}$ to $\bold{x}$, $\bold{y}$, $\bold{z}$.
或者，我们可以将相同的转换视为首先将 $\bold{e}$ 移动到原点，然后将 $\bold{u}$、$\bold{v}$、$\bold{w}$ 与 $  \bold{x}$、$\bold{y}$、$\bold{z}$对齐。

To make our previously z-axis-only viewing algorithm work for cameras with any location and orientation, we just need to add this camera transformation to  the product of the viewport and projection transformations, so that it converts the incoming points from world to camera coordinates before they are projected:
为1了使我们之前的仅 z 轴查看算法适用于任何位置和方向的相机，我们只需将此相机变换添加到视口和投影变换的乘积中，以便它将输入点从世界坐标转换为相机坐标 在预测之前：
<img src=".\Images\Figure 7.6_1.png" alt="Figure 7.6_1" style="zoom:67%;" />

Again, almost no code is needed once the matrix infrastructure is in place. 
同样，一旦矩阵基础设施就位，几乎不需要任何代码。

## 7.2 Projective Transformations 投影变换

We have left perspective for last because it takes a little bit of cleverness to make it fit into the system of vectors and matrix transformations that has served us so well up to now. To see what we need to do, let’s look at what the perspective projection transformation needs to do with points in camera space. Recall that the  viewpoint is positioned at the origin and the camera is looking along the z-axis.
我们把透视图留到最后，因为它需要一点点聪明才智才能使其适应迄今为止为我们提供良好服务的向量和矩阵变换系统。 为了了解我们需要做什么，让我们看看透视投影变换需要对相机空间中的点做什么。 回想一下，视点位于原点，相机沿着 z 轴观察。

> For the moment we will ignore the sign of z to keep the equations simpler, but it will return on page 150. 
> 目前我们将忽略 z 的符号以使方程更简单，但它将在第 150 页返回。

The key property of perspective is that the size of an object on the screen is proportional to $1/z$ for an eye at the origin looking up the negative z-axis. This can be expressed more precisely in an equation for the geometry in Figure 7.8: 
透视的关键属性是，对于在原点处向上看负 z 轴的眼睛，屏幕上对象的大小与 $1/z$ 成正比。 这可以用图 7.8 中的几何方程更精确地表达：
$$
y_s = \frac{d}{z}y,\ \ \ \ (7.5)
$$
<img src=".\Images\Figure 7.8.png" alt="Figure 7.8" style="zoom:67%;" />
Figure 7.8. The geometry for Equation (7.5). The viewer’s eye is at $\bold{e}$ and the gaze direction is $\bold{g}$ (the minus z-axis). The view plane is a distance $d$ from the eye. A point is projected toward $\bold{e}$ and where it intersects the view plane is where it is drawn. 
图 7.8. 方程（7.5）的几何形状。 观看者的眼睛位于$\bold{e}$，注视方向为$\bold{g}$（负z轴）。 视平面距眼睛的距离为$d$。 一个点向 $\bold{e}$ 投影，它与视图平面相交的地方就是它被绘制的地方。

where $y$ is the distance of the point along the $y$-axis, and $y_s$ is where the point should be drawn on the screen. 
其中 $y$ 是点沿 $y$ 轴的距离，$y_s$ 是应在屏幕上绘制点的位置。

We would really like to use the matrix machinery we developed for orthographic projection to draw perspective images; we could then just multiply another matrix into our composite matrix and use the algorithm we already have. However, this type of transformation, in which one of the coordinates of the input vector appears in the denominator, can’t be achieved using affine transformations. 
我们真的很想使用我们为正交投影开发的矩阵机制来绘制透视图像； 然后我们可以将另一个矩阵乘以我们的复合矩阵并使用我们已有的算法。 然而，这种类型的变换（其中输入向量的坐标之一出现在分母中）无法使用仿射变换来实现。

We can allow for division with a simple generalization of the mechanism of homogeneous coordinates that we have been using for affine transformations. We have agreed to represent the point $(x, y, z)$ using the homogeneous vector $[x\ y\ z\ 1]^T$; the extra coordinate, $w$, is always equal to 1, and this is ensured by always using $[0\ 0\ 0\ 1]^T$ as the fourth row of an affine transformation matrix. 
我们可以通过对我们一直用于仿射变换的齐次坐标机制的简单概括来允许除法。 我们同意使用齐次向量 $[x\ y\ z\ 1]^T$ 来表示点 $(x, y, z)$； 额外的坐标 $w$ 始终等于 1，这是通过始终使用 $[0\ 0\ 0\ 1]^T$ 作为仿射变换矩阵的第四行来确保的。

Rather than just thinking of the 1 as an extra piece bolted on to coerce matrix multiplication to implement translation, we now define it to be the denominator of the $x-$, $y-$, and $z-$coordinates: the homogeneous vector $[x\ y\ z\ w]^T$ represents the point $(x/w, y/w, z/w)$. This makes no difference when $w = 1$, but it allows a broader range of transformations to be implemented if we allow any values in the bottom row of a transformation matrix, causing $w$ to take on values other than 1. 
我们现在将其定义为 $x-$、$y-$ 和 $z-$ 坐标的分母，而不是仅仅将 1 视为附加在强制矩阵乘法上以实现平移的额外部分：齐次 向量$[x\ y\ z\ w]^T$表示点$(x/w, y/w, z/w)$。 当 $w = 1$ 时，这没有什么区别，但如果我们允许变换矩阵底行中的任何值，导致 $w$ 取 1 以外的值，则可以实现更广泛的变换。

Concretely, linear transformations allow us to compute expressions like
具体来说，线性变换允许我们计算如下表达式
$x' = ax + by + cz  $

and affine transformations extend this to
仿射变换将其扩展到
$x' = ax + by + cz + d  $

Treating $w$ as the denominator further expands the possibilities, allowing us to compute functions like
将 $w$ 视为分母进一步扩展了可能性，使我们能够计算如下函数
$x' = \frac{ax + by + cz + d  }{ex + fy + gz + h  } \\$ 

this could be called a “linear rational function” of x, y, and z. But there is an extra constraint—the denominators are the same for all coordinates of the transformed point: 
这可以称为 x、y 和 z 的“线性有理函数”。 但有一个额外的约束 - 变换点的所有坐标的分母都相同：
$$
x' = \frac{a_1x + b_1y + c_1z + d_1}{ex + fy + gz + h} \\
y' = \frac{a_2x + b_2y + c_2z + d_2}{ex + fy + gz + h} \\
z' = \frac{a_3x + b_3y + c_3z + d_3}{ex + fy + gz + h} \\
$$
Expressed as a matrix transformation, 
表示为矩阵变换，
$$
\ \begin{bmatrix}
\tilde{x} \\
\tilde{y} \\
\tilde{z} \\
\tilde{w}
\end{bmatrix} = 
\begin{bmatrix}
a_1 & b_1 & c_1 & d_1 \\
a_2 & b_2 & c_2 & d_2 \\
a_3 & b_3 & c_3 & d_3 \\
e & f & g & h
\end{bmatrix}
\begin{bmatrix}
x \\
y\\
z \\
1
\end{bmatrix} \\
(x', y', z') = (\tilde{x}/\tilde{w}, \tilde{y}/ \tilde{w}, \tilde{z}/ \tilde{w})
$$
A transformation like this is known as a projective transformation or a homography. 
像这样的变换称为投影变换或单应性。

Example. The matrix
例子。 矩阵
$$
\bold{M} = \begin{bmatrix}
 2 & 0 & -1 \\
 0 & 3 & 0  \\
 0 & \frac{2}{3} & \frac{1}{3}
\end{bmatrix}
$$
represents a 2D projective transformation that transforms the unit square $([0, 1] × [0, 1])$ to the quadrilateral shown in Figure 7.9. 
表示一个 2D 投影变换，将单位正方形 $([0, 1] × [0, 1])$ 变换为图 7.9 所示的四边形。

![Figure 7.9](.\Images\Figure 7.9.png)
Figure 7.9. A projective transformation maps a square to a quadrilateral, preserving straight lines but not parallel lines. 
图 7.9. 射影变换将正方形映射为四边形，保留直线但不保留平行线。

For instance, the lower-right corner of the square at (1, 0) is represented by the homogeneous vector $[1\ 0\ 1]^T$ and transforms as follows: 
例如，(1, 0) 处的正方形右下角由齐次向量 $[1\ 0\ 1]^T$ 表示，并变换如下：
$$
\begin{bmatrix}
2 & 0 & -1 \\
0 & 3 & 0 \\
0 & \frac{2}{3} & \frac{1}{3}
\end{bmatrix}
\begin{bmatrix}
1 \\
0 \\
1
\end{bmatrix}
= \begin{bmatrix}
1 \\
0 \\
\frac{1}{3}
\end{bmatrix}
$$
which represents the point $(1/ \frac{1}{3}, 0/\frac{1}{3})$, or $(3, 0)$. Note that if we use the matrix
表示点 $(1/ \frac{1}{3}, 0/\frac{1}{3})$ 或 $(3, 0)$。 请注意，如果我们使用矩阵
$$
3\bold{M} = \begin{bmatrix}
6 & 0 & -3 \\
0 & 9 & 0 \\
0 & 2 & 1
\end{bmatrix}
$$
instead, the result is $[3\ 0\ 1]^T$, which also represents $(3, 0)$. In fact, any scalar multiple $c\bold{M}$ is equivalent: the numerator and denominator are both scaled by $c$, which does not change the result. 
相反，结果是 $[3\ 0\ 1]^T$，它也代表 $(3, 0)$。 事实上，任何标量倍数 $c\bold{M}$ 都是等价的：分子和分母都按 $c$ 缩放，这不会改变结果。

There is a more elegant way of expressing the same idea, which avoids treating the w-coordinate specially. In this view a 3D projective transformation is simply a 4D linear transformation, with the extra stipulation that all scalar multiples of a vector refer to the same point: 
有一种更优雅的方式来表达相同的想法，从而避免特殊处理 w 坐标。 在此视图中，3D 投影变换只是 4D 线性变换，额外规定向量的所有标量倍数都指向同一点：
$\bold{x} ∼ α\bold{x}\ for\ all\ α\ ≠\ 0.  $

The symbol ∼ is read as “is equivalent to” and means that the two homogeneous vectors both describe the same point in space. 
符号 ∼ 被理解为“等于”，意味着两个齐次向量都描述空间中的同一点。

**Example.** In 1D homogeneous coordinates, in which we use 2-vectors to represent points on the real line, we could represent the point (1.5) using the homogeneous vector $[1.5\ 1]^T$, or any other point on the line $x = 1.5h$ in homogeneous space. (See Figure 7.10.)
**示例。** 在一维齐次坐标中，我们使用 2 向量来表示实线上的点，我们可以使用齐次向量 $[1.5\ 1]^T$ 或任意向量来表示点 (1.5) 齐次空间中直线 $x = 1.5h$ 上的其他点。 （见图 7.10。）
<img src=".\Images\Figure 7.10.png" alt="Figure 7.10" style="zoom:67%;" />
Figure 7.10. The point $x = 1.5$ is represented by any point on the line $x = 1.5h$, such as points at the hollow circles. However, before we interpret $x$ as a conventional Cartesian coordinate, we first divide by $h$ to get $(x, h) = (1.5,1)$ as shown by the black point. 
图 7.10. 点 $x = 1.5$ 由直线 $x = 1.5h$ 上的任意点表示，例如空心圆处的点。 然而，在我们将 $x$ 解释为传统的笛卡尔坐标之前，我们首先除以 $h$ 得到 $(x, h) = (1.5,1)$，如黑点所示。

In 2D homogeneous coordinates, in which we use 3-vectors to represent points in the plane, we could represent the point $(-1, -0.5)$ using the homogeneous vector $[-2;\ -1;\ 2]^T$, or any other point on the line $\bold{x} = α[-1\ -0.5\ 1]^T$. Any homogeneous vector on the line can be mapped to the line’s intersection with the plane $w = 1$ to obtain its Cartesian coordinates. (See Figure 7.11.)
在二维齐次坐标中，我们使用3向量来表示平面上的点，我们可以用齐次向量$[-2;\ -1;\ 2]^T$来表示点$(-1，-0.5)$，或者直线上的任何其他点$\bold{x} = α[-1\ -0.5\ 1]^T$。直线上的任何齐次向量都可以映射到直线与平面$w = 1$的交点，从而得到直线的笛卡尔坐标。(见图7.11)
<img src=".\Images\Figure 7.10.png" alt="Figure 7.10" style="zoom:67%;" />
Figure 7.11. A point in homogeneous coordinates is equivalent to any other point on the line through it and the origin, and normalizing the point amounts to intersecting this line with the plane $w = 1$. 
图7.11. 齐次坐标中的一个点等价于直线上通过它和原点的任何其他点，将该点归一化等于将这条直线与平面$w = 1$相交。

It’s fine to transform homogeneous vectors as many times as needed, without worrying about the value of the w-coordinate—in fact, it is fine if the wcoordinate is zero at some intermediate phase. It is only when we want the ordinary Cartesian coordinates of a point that we need to normalize to an equivalent point that has $w = 1$, which amounts to dividing all the coordinates by $w$. Once we’ve done this we are allowed to read off the (x, y, z)-coordinates from the first three components of the homogeneous vector.
可以根据需要多次变换齐次向量，而不必担心 w 坐标的值 - 事实上，如果 w 坐标在某个中间阶段为零也很好。 只有当我们想要一个点的普通笛卡尔坐标时，我们才需要将其归一化为 $w = 1$ 的等效点，这相当于将所有坐标除以 $w$。 完成此操作后，我们就可以从齐次向量的前三个分量中读取 (x, y, z) 坐标。

## 7.3 Perspective Projection 透视投影

The mechanism of projective transformations makes it simple to implement the division by z required to implement perspective. In the 2D example shown in Figure 7.8, we can implement the perspective projection with a matrix transformation as follows: 
投影转换的机制使得实现透视所需的除以z的方法变得简单。在图7.8所示的2D示例中，我们可以通过如下的矩阵变换来实现透视投影:
$$
\begin{bmatrix}
y_s \\
1
\end{bmatrix}
∼ \begin{bmatrix}
d & 0 & 0 \\
0 & 1 & 0
\end{bmatrix}
\begin{bmatrix}
y \\
z \\
1
\end{bmatrix}
$$
This transforms the 2D homogeneous vector $[y;\ z;\ 1]^T$ to the 1D homogeneous vector $[dy\ z]^T$, which represents the 1D point $(dy/z)$ (because it is equivalent to the 1D homogeneous vector $[dy/z 1]^T$. This matches Equation (7.5). 
这将二维齐次向量$[y;\ z;\ 1]^T$变换为一维齐次向量$[dy\ z]^T$，它表示一维点$(dy/z)$(因为它等价于一维齐次向量$[dy/z]^T$)。这符合式(7.5)。

For the “official” perspective projection matrix in 3D, we’ll adopt our usual convention of a camera at the origin facing in the $-z$ direction, so the distance of the point $(x, y, z)$ is $-z$. As with orthographic projection, we also adopt the notion of near and far planes that limit the range of distances to be seen. In this context, we will use the near plane as the projection plane, so the image plane distance is $-n$.
对于3D中的“官方”透视投影矩阵，我们将采用通常的惯例，即在原点处面向$-z$方向设置摄像机，因此点$(x, y, z)$的距离为$-z$。与正射影一样，我们也采用了远近平面的概念，这限制了可以看到的距离范围。在这种情况下，我们将使用近平面作为投影平面，因此成像平面距离为$-n$。

> Remember, n < 0. 
> 请记住，n < 0。

The desired mapping is then $y_s = (n/z)y$, and similarly for $x$. This transformation can be implemented by the perspective matrix:
所需的映射是$y_s = (n/z)y$，对于$x$也是如此。这个变换可以通过透视矩阵来实现:
$$
\bold{P} = \begin{bmatrix}
n & 0 & 0 & 0 \\
0 & n & 0 & 0 \\
0 & 0 & n + f & -fn \\
0 & 0 & 1 & 0
\end{bmatrix}
$$
The first, second, and fourth rows simply implement the perspective equation. The third row, as in the orthographic and viewport matrices, is designed to bring the z-coordinate “along for the ride” so that we can use it later for hidden surface removal. In the perspective projection, though, the addition of a non-constant denominator prevents us from actually preserving the value of z—it’s actually impossible to keep $z$ from changing while getting $x$ and $y$ to do what we need them to do. Instead we’ve opted to keep $z$ unchanged for points on the near or far planes. 
第一行、第二行和第四行简单地实现了透视图方程。第三行，就像在正射影和视口矩阵中一样，旨在将z坐标“随驾而行”，以便我们可以稍后使用它来删除隐藏表面。然而，在透视投影中，非常数分母的加入阻止了我们实际保留z的值——实际上不可能在保持z不变的同时让x和y做我们需要它们做的事情。相反，我们选择保持近平面或远平面上的点$z$不变。

> More on this later. 
> 稍后会详细介绍。

There are many matrices that could function as perspective matrices, and all of them nonlinearly distort the z-coordinate. This specific matrix has the nice properties shown in Figures 7.12 and 7.13; it leaves points on the $(z = n)$-plane entirely alone, and it leaves points on the $(z = f)$-plane while “squishing” them in $x$ and $y$ by the appropriate amount. The effect of the matrix on a point $(x, y, z)$ is
有许多矩阵可以作为透视矩阵，它们都非线性地扭曲了z坐标。这个特定的矩阵具有如图7.12和7.13所示的良好性质;它将点完全单独留在$(z = n)$-平面上，并将点留在$(z = f)$-平面上，同时将它们适当地“压扁”到$x$和$y$中。矩阵对点$(x, y, z)$的影响是
$$
\bold{P}\begin{bmatrix}
x \\ y \\ z \\1
\end{bmatrix}
= \begin{bmatrix} nx \\ ny \\ (n + f)z -fn \\ z  \end{bmatrix}
∼ \begin{bmatrix} \frac{nx}{z} \\ \frac{ny}{z} \\ n + f- \frac{fn}{z} \\ 1 \end{bmatrix}
$$
<img src=".\Images\Figure 7.12.png" alt="Figure 7.12" style="zoom: 50%;" />
Figure 7.12. The perspective projection leaves points on the $z = n$ plane unchanged and maps the large $z = f$ rectangle at the back of the perspective volume to the small $z = f$ rectangle at the back of the orthographic volume. 
图7.12. 透视投影使$z = n$平面上的点保持不变，并将透视体后面的大$z = f$矩形映射到正射影体后面的小$z = f$矩形。

<img src=".\Images\Figure 7.13.png" alt="Figure 7.13" style="zoom:67%;" />
Figure 7.13. The perspective projection maps any line through the origin/eye to a line parallel to the z-axis and without moving the point on the line at $z = n$.
图 7.13. 透视投影将通过原点/眼睛的任何线映射到与 z 轴平行的线，并且不移动线上 $z = n$ 处的点。

As you can see, x and y are scaled and, more importantly, divided by $z$. Because both n and z (inside the view volume) are negative, there are no “flips” in $x$ and $y$. Although it is not obvious (see the exercise at the end of the chapter), the transform also preserves the relative order of $z$ values between $z = n$ and $z = f$, allowing us to do depth ordering after this matrix is applied. This will be important later when we do hidden surface elimination.
正如你所看到的，x和y被缩放了，更重要的是，被除以z。因为n和z(在视图体积内)都是负的，所以$x$和$y$中没有“翻转”。虽然这并不明显(参见本章末尾的练习)，但变换也保留了$z$值在$z = n$和$z = f$之间的相对顺序，允许我们在应用该矩阵后进行深度排序。这在后面进行隐藏面消去时非常重要。

Sometimes we will want to take the inverse of $\bold{P}$, for example, to bring a screen coordinate plus z back to the original space, as we might want to do for picking. The inverse is
有时我们想取$\bold{P}$的逆，例如，将屏幕坐标+ z带回到原始空间，就像我们在选择时可能想做的那样。逆函数是
$$
\bold{P}^{-1} = \begin{bmatrix}
\frac{1}{n} & 0 & 0 & 0 \\
0 & \frac{1}{n} & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & -\frac{1}{fn} & \frac{n+f}{fn}
\end{bmatrix}
$$
Since multiplying a homogeneous vector by a scalar does not change its meaning, the same is true of matrices that operate on homogeneous vectors. So we can write the inverse matrix in a prettier form by multiplying through by $nf$:
由于一个齐次向量乘以一个标量不会改变它的意义，所以对于作用于齐次向量的矩阵也是如此。我们可以把逆矩阵写成更漂亮的形式通过乘以$nf$
$$
\bold{P}^{-1} = \begin{bmatrix}
f & 0 & 0 & 0 \\
0 & f & 0 & 0 \\
0 & 0 & 0 & fn \\
0 & 0 & -1 & n + f
\end{bmatrix}
$$
This matrix is not literally the inverse of the matrix $\bold{P}$, but the transformation it describes is the inverse of the transformation described by $\bold{P}$. 
这个矩阵并不是字面上的矩阵 $\bold{P}$ 的逆矩阵，但它描述的变换是 $\bold{P}$ 描述的变换的逆矩阵。

Taken in the context of the orthographic projection matrix $\bold{M}_{orth}$ in Equation (7.3), the perspective matrix simply maps the perspective view volume (which is shaped like a slice, or frustum, of a pyramid) to the orthographic view volume (which is an axis-aligned box). The beauty of the perspective matrix is that once we apply it, we can use an orthographic transform to get to the canonical view volume. Thus, all of the orthographic machinery applies, and all that we have added is one matrix and the division by w. It is also heartening that we are not “wasting” the bottom row of our four by four matrices!
在式(7.3)中的正交投影矩阵$\bold{M}_{north}$的上下文中，透视矩阵简单地将透视视图体(其形状类似于金字塔的切片或截锥体)映射到正交视图体(它是一个与轴对齐的盒子)。透视矩阵的美妙之处在于，一旦我们应用了它，我们就可以使用正交变换来获得规范视图体积。因此，所有的正字法机制都适用，我们所添加的只是一个矩阵和除以w。同样令人鼓舞的是，我们没有“浪费”我们的4 × 4矩阵的底部行!

Concatenating $\bold{P}$ with $\bold{M}_{orth}$ results in the perspective projection matrix, 
将$\bold{P}$与$\bold{M}_{north}$连接得到透视投影矩阵，
$\bold{M}_{per} = \bold{M}_{orth}\bold{P}$

One issue, however, is: How are $l,r,b,t$ determined for perspective? They identify the “window” through which we look. Since the perspective matrix does not change the values of $x$ and $y$ on the $(z = n)$-plane, we can specify $(l, r, b, t)$ on that plane.
然而，有一个问题是:$ 1,r,b,t$是如何决定透视图的?它们确定了我们观看的“窗口”。由于透视矩阵不会改变$(z = n)$-平面上的$x$和$y$的值，因此我们可以在该平面上指定$(l, r, b, t)$。

To integrate the perspective matrix into our orthographic infrastructure, we simply replace $\bold{M}_{orth}$ with $\bold{M}_{per}$, which inserts the perspective matrix $\bold{P}$ after the camera matrix $\bold{M}_{cam}$ has been applied but before the orthographic projection. So the full set of matrices for perspective viewing is
要将透视矩阵集成到我们的正交基础结构中，我们只需将 $\bold{M}_{orth}$ 替换为 $\bold{M}_{per}$，这会在后面插入透视矩阵 $\bold{P}$ 相机矩阵 $\bold{M}_{cam}$ 已应用，但在正交投影之前。 所以透视观察的全套矩阵是
$\bold{M} = \bold{M}_{vp}\bold{M}_{orth}\bold{P}\bold{M}_{cam}.  $

The resulting algorithm is: 
得到的算法是：

> compute $\bold{M}_{vp}$
> compute $\bold{M}_{per}$
> compute $\bold{M}_{cam}$
> $\bold{M} = \bold{M}_{vp}\bold{M}_{per}\bold{M}_{cam}$
> for each line segment $(\bold{a}_i, \bold{b}_i)$ do
> 	p = $\bold{M}\bold{a}_i$
> 	q = $\bold{M}\bold{b}_i$
> 	drawline$(x_p/w_p, y_p/w_p, x_q/w_q, y_q/w_q)$

Note that the only change other than the additional matrix is the divide by the homogeneous coordinate $w$.
注意，除了额外的矩阵之外，唯一的变化是除以齐次坐标w。

Multiplied out, the matrix $\bold{M}_{per}$ looks like this: 
乘出来，矩阵$\bold{M}_{per}$看起来像这样: 
$$
\bold{M}_{per} = \begin{bmatrix}
\frac{2n}{r - l} & 0 & \frac{l + r}{l - r} & 0 \\
0 & \frac{2n}{t - b} & \frac{b + t}{b - t} & 0 \\
0 & 0 & \frac{f + n}{n - f} & \frac{2fn}{f - n} \\
0 & 0 & 1 & 0 \\
\end{bmatrix}
$$
This or similar matrices often appear in documentation, and they are less mysterious when one realizes that they are usually the product of a few simple matrices.
这个或类似的矩阵经常出现在文档中，当人们意识到它们通常是几个简单矩阵的乘积时，它们就不那么神秘了。

Example. Many APIs such as OpenGL (Shreiner, Neider, Woo, & Davis, 2004) use the same canonical view volume as presented here. They also usually have the user specify the absolute values of $n$ and $f$. The projection matrix for OpenGL is
例子。 许多 API，例如 OpenGL（Shreiner、Neider、Woo 和 Davis，2004）使用与此处介绍的相同的规范视图体积。 他们通常还让用户指定 $n$ 和 $f$ 的绝对值。 OpenGL 的投影矩阵为 
$$
\bold{M}_{OpenGL} = \begin{bmatrix}
\frac{2|n|}{r - l} & 0 & \frac{r + l}{r - l} & 0 \\
0 & \frac{2|n|}{t - b} & \frac{t + b}{t - b} & 0 \\
0 & 0 & \frac{|n| + |f|}{|n| - |f|} & \frac{2|f||n|}{|n| - |f|} \\
0 & 0 & -1 & 0 \\
\end{bmatrix}
$$
Other APIs send n and f to 0 and 1, respectively. Blinn (J. Blinn, 1996) recommends making the canonical view volume $[0, 1]^3$ for efficiency. All such decisions will change the the projection matrix slightly. 
其他API分别将n和f发送到0和1。Blinn (J. Blinn, 1996)建议为提高效率而创建规范视图卷$[0,1]^3$。所有这些决定都会稍微改变投影矩阵。

## 7.4 Some Properties of the Perspective Transform 透视变换的一些属性

An important property of the perspective transform is that it takes lines to lines and planes to planes. In addition, it takes line segments in the view volume to line segments in the canonical volume. To see this, consider the line segment 
透视变换的一个重要性质是它将线转换为线，将平面转换为平面。此外，它将视图卷中的线段转换为规范卷中的线段。为了理解这一点，考虑一下线段
$\bold{q} + t(\bold{Q} - \bold{q})$

When transformed by a 4 ×4 matrix $\bold{M}$, it is a point with possibly varying homogeneous coordinate: 
当用4 ×4矩阵$\bold{M}$变换时，它是一个可能具有变化齐次坐标的点: 
$\bold{M}{q} + t(\bold{M}\bold{Q} - \bold{M}\bold{q}) ≡ \bold{r} + t(\bold{R} - \bold{r}).  $

The homogenized 3D line segment is 
均质化 3D 线段为
$$
\frac{\bold{r} + t(\bold{R} − \bold{r})}{w_r + t(w_R − w_r)} \ \ \ \ (7.6)
$$
If Equation (7.6) can be rewritten in a form 
若式(7.6)可以改写为
$$
\frac{\bold{r}}{w_r} + f(t)(\frac{\bold{R}}{w_R} - \frac{\bold{r}}{w_r}) \ \ \ \ \ (7.7)
$$
then all the homogenized points lie on a 3D line. Brute force manipulation of Equation (7.6) yields such a form with
那么所有均匀化的点都在一条三维直线上。蛮力操作公式(7.6)产生这样的形式
$$
f(t) = \frac{w_Rt}{w_r + t(w_R − w_r)} \ \ \ \ \ (7.8)
$$
It also turns out that the line segments do map to line segments preserving the ordering of the points (Exercise 8), i.e., they do not get reordered or “torn.”
结果还表明，线段确实映射到保持点的顺序的线段(练习8)，也就是说，它们不会被重新排序或“撕裂”。

A byproduct of the transform taking line segments to line segments is that it takes the edges and vertices of a triangle to the edges and vertices of another triangle. Thus, it takes triangles to triangles and planes to planes. 
将线段转换为线段的一个副产品是，它将一个三角形的边和顶点转换为另一个三角形的边和顶点。因此，它将三角形转换为三角形，将平面转换为平面。 

## 7.5 Field-of-View 视场

While we can specify any window using the (l, r, b, t) and n values, sometimes we would like to have a simpler system where we look through the center of the window. This implies the constraint that
虽然我们可以使用(l, r, b, t)和n值指定任何窗口，但有时我们希望有一个更简单的系统，通过窗口的中心查看。这意味着约束条件
$l = -r \\
b = -t$

If we also add the constraint that the pixels are square, i.e., there is no distortion of shape in the image, then the ratio of $r$ to $t$ must be the same as the ratio of the number of horizontal pixels to the number of vertical pixels: 
如果我们还加上像素是正方形的约束，即图像中没有形状畸变，那么$r$与$t$的比值必须等于水平像素与垂直像素的比值:
$\frac{n_x}{n_y} = \frac{r}{t} \\ $

Once $n_x$ and $n_y$ are specified, this leaves only one degree of freedom. That is often set using the field-of-view shown as $θ$ in Figure 7.14. This is sometimes called the vertical field-of-view to distinguish it from the angle between left and right sides or from the angle between diagonal corners. From the figure we can see that
一旦指定了$n_x$和$n_y$，就只剩下一个自由度了。这通常使用图7.14中显示的视场$θ$来设置。这有时被称为垂直视场，以区别于左右两边的角度或对角角之间的角度。从图中我们可以看到
$\tan \frac{θ}{2} = \frac{t}{|n|}\\ $

If $n$ and $θ$ are specified, then we can derive $t$ and use code for the more general viewing system. In some systems, the value of $n$ is hard-coded to some reasonable value, and thus we have one fewer degree of freedom. 
如果指定了$n$和$θ$，那么我们可以导出$t$，并使用代码用于更一般的查看系统。在某些系统中，$n$的值被硬编码为某个合理的值，这样我们就少了一个自由度。

## Frequently Asked Questions 常见问题

### Is orthographic projection ever useful in practice? 正射影在实践中有用吗?

It is useful in applications where relative length judgments are important. It can also yield simplifications where perspective would be too expensive as occurs in some medical visualization applications.
它在相对长度判断很重要的应用程序中很有用。在某些医学可视化应用程序中，透视图的使用成本太高，而这种方法也可以简化透视图。

### The tessellated spheres I draw in perspective look like ovals. Is this a bug? 我在透视图中画的镶嵌球体看起来像椭圆形。这是臭虫吗?

No. It is correct behavior. If you place your eye in the same relative position to the screen as the virtual viewer has with respect to the viewport, then these ovals will look like circles because they themselves are viewed at an angle. 
不。这是正确的行为。如果你把你的眼睛放在与屏幕相同的相对位置上，就像虚拟观看者相对于视口的位置一样，那么这些椭圆看起来就像圆圈，因为它们本身是在一个角度上被观看的。

### Does the perspective matrix take negative z values to positive z values with a reversed ordering? Doesn’t that cause trouble? 透视矩阵是否以相反的顺序将负 z 值变为正 z 值？ 这不会带来麻烦吗？

Yes. The equation for transformed z is 
是的。 z 变换后的方程为
$z' = n + f - \frac{fn}{z} \\ $

So $z = +\epsilon$ is transformed to $z' = -∞$ and $z = -\epsilon$ is transformed to $z = ∞$. So any line segments that span $z = 0$ will be “torn” although all points will be projected to an appropriate screen location. This tearing is not relevant when all objects are contained in the viewing volume. This is usually assured by clipping to the view volume. However, clipping itself is made more complicated by the tearing phenomenon as is discussed in Chapter 8.
因此 $z = +\epsilon$ 转换为 $z' = -∞$ 并且 $z = -\epsilon$ 转换为 $z = ∞$。 因此，尽管所有点都将投影到适当的屏幕位置，但跨越 $z = 0$ 的任何线段都将被“撕裂”。 当所有对象都包含在观看体积中时，这种撕裂是不相关的。 这通常通过剪切到视图体积来保证。 然而，如第 8 章中讨论的那样，撕裂现象使剪切本身变得更加复杂。

### The perspective matrix changes the value of the homogeneous coordinate. Doesn’t that make the move and scale transformations no longer work properly? 透视矩阵改变齐次坐标的值。 这难道不会导致移动和规模转换不再正常进行吗？

Applying a translation to a homogeneous point we have 
将平移应用到齐次点我们有
$$
\begin{bmatrix}
1 & 0 & 0 & t_x \\
0 & 1 & 0 & t_y \\
0 & 0 & 1 & t_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
hx \\ hy \\ hz \\ h
\end{bmatrix}
= \begin{bmatrix}
hx + ht_x \\ hy + ht_y \\ hz + ht_z \\ h
\end{bmatrix} \rightarrow{homogenize} 
\begin{bmatrix}
x + t_x \\
y + t_y \\
Z + t_z \\
1
\end{bmatrix}
$$
Similar effects are true for other transforms (see Exercise 5). 
其他变换也有类似的效果（参见练习 5）。

## Notes 注释

Most of the discussion of viewing matrices is based on information in Real-Time Rendering (Akenine-M¨ oller et al., 2008), the OpenGL Programming Guide (Shreiner et al., 2004), Computer Graphics (Hearn & Baker, 1986), and 3D Game Engine Design (Eberly, 2000).
大多数关于查看矩阵的讨论都是基于实时渲染（Akenine-Měller 等人，2008 年）、OpenGL 编程指南（Shreiner 等人，2004 年）、计算机图形学（Hearn & Baker，1986 年）中的信息 ）和 3D 游戏引擎设计（Eberly，2000）。

## Exercises

1.  Construct the viewport matrix required for a system in which pixel coordinates count down from the top of the image, rather than up from the bottom.
   构建系统所需的视口矩阵，其中像素坐标从图像顶部向下计数，而不是从底部向上计数。
2. Multiply the viewport and orthographic projection matrices, and show that the result can also be obtained by a single application of Equation (6.7). 
   将视口矩阵和正交投影矩阵相乘，并表明结果也可以通过单独应用方程（6.7）来获得。
3. Derive the third row of Equation (7.3) from the constraint that z is preserved for points on the near and far planes.
   从近平面和远平面上的点保留 z 的约束导出方程（7.3）的第三行。
4. Show algebraically that the perspective matrix preserves order of z values within the view volume.
    用代数方式表明透视矩阵保留视图体积内 z 值的顺序。
5. For a 4×4 matrix whose top three rows are arbitrary and whose bottom row is $(0, 0, 0, 1)$, show that the points $(x, y, z, 1)$ and $(hx, hy, hz, h)$ transform to the same point after homogenization.
    对于一个 4×4 矩阵，其前三行是任意的，其底行是 $(0, 0, 0, 1)$，证明点 $(x, y, z, 1)$ 和 $(hx , hy, hz, h)$均质化后变换到同一点。
6. Verify that the form of $\bold{M}^{−1}_p$ given in the text is correct.
   验证文中给出的$\bold{M}^{−1}_p$的形式是否正确。
7. Verify that the full perspective to canonical matrix $\bold{M}_{projection}$ takes $(r, t, n)$ to $(1, 1, 1)$.
    验证规范矩阵 $\bold{M}_{projection}$ 的完整视角是否从 $(r, t, n)$ 变为 $(1, 1, 1)$。
8. Write down a perspective matrix for $n = 1$, $f = 2$.
   写出 $n = 1$、$f = 2$ 的透视矩阵。
9. For the point $\bold{p} = (x, y, z, 1)$, what are the homogenized and unhomogenized results for that point transformed by the perspective matrix in Exercise 6?
   对于点 $\bold{p} = (x, y, z, 1)$，练习 6 中透视矩阵变换该点的均质化和非均质化结果是多少？
10. For the eye position $\bold{e} = (0, 1, 0)$, a gaze vector $\bold{g} = (0, −1, 0)$, and a viewup vector $\bold{t} = (1, 1, 0)$, what is the resulting orthonormal $\bold{uvw}$ basis used for coordinate rotations?
    对于眼睛位置 $\bold{e} = (0, 1, 0)$，注视向量 $\bold{g} = (0, −1, 0)$ 和视图向量 $\bold{ t} = (1, 1, 0)$，用于坐标旋转的正交 $\bold{uvw}$ 基础是什么？
11. Show, that for a perspective transform, line segments that start in the view volume do map to line segments in the canonical volume after homogenization. Further, show that the relative ordering of points on the two segments is the same. Hint: Show that the f(t) in Equation (7.8) has the properties
    $f(0) = 0, f(1) = 1$, the derivative of f is positive for all $t ∈ [0, 1]$, and the homogeneous coordinate does not change sign.
    表明，对于透视变换，在视图体积中开始的线段在均质化后确实映射到规范体积中的线段。 进一步证明两条线段上点的相对顺序是相同的。 提示：证明方程（7.8）中的 f(t) 具有以下性质
         $f(0) = 0, f(1) = 1$，f的导数对于所有$t ∈ [0, 1]$均为正，且齐次坐标不改变符号。