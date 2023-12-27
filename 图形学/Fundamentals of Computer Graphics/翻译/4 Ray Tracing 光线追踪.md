# 4 Ray Tracing  光线追踪

One of the basic tasks of computer graphics is rendering three-dimensional objects: taking a scene, or model, composed of many geometric objects arranged in 3D space and producing a 2D image that shows the objects as viewed from a particular viewpoint. It is the same operation that has been done for centuries by architects and engineers creating drawings to communicate their designs to others. 
计算机图形学的基本任务之一是渲染三维对象：将一个场景或模型，由许多在三维空间中排列的几何对象组成，转化为一个显示这些对象的二维图像，从而展示它们在特定视角下的外观。这个操作类似于几个世纪以来建筑师和工程师为了向他人传达设计而进行的绘图工作。

Fundamentally, rendering is a process that takes as its input a set of objects and produces as its output an array of pixels. One way or another, rendering involves  considering how each object contributes to each pixel; it can be organized in two general ways. In object-order rendering, each object is considered in turn, and for each object all the pixels that it influences are found and updated. In image-order rendering, each pixel is considered in turn, and for each pixel all the objects that influence it are found and the pixel value is computed. You can think of the difference in terms of the nesting of loops: in image-order rendering the “for each pixel” loop is on the outside, whereas in object-order rendering the “for each object” loop is on the outside. 
从根本上说，渲染是一个以一组对象作为输入并生成一组像素作为输出的过程。以某种方式，渲染涉及考虑每个对象如何影响每个像素；它可以以两种一般的方式组织。在对象顺序渲染中，逐个考虑每个对象，对于每个对象，找到并更新其影响的所有像素。在图像顺序渲染中，逐个考虑每个像素，对于每个像素，找到影响它的所有对象，并计算像素值。你可以从循环的嵌套角度来思考这种差异：在图像顺序渲染中，“对于每个像素”的循环在外部，而在对象顺序渲染中，“对于每个对象”的循环在外部。

> If the output is a vector image rather than a raster image, rendering doesn’t have to involve pixels, but we’ll assume raster images in this book. 
> 如果输出是矢量图像而不是光栅图像，则渲染不必涉及像素，但我们将在本书中假设光栅图像。

Image-order and object-order rendering approaches can compute exactly the same images, but they lend themselves to computing different kinds of effects and have quite different performance characteristics. We’ll explore the comparative strengths of the approaches in Chapter 8 after we have discussed them both, but, broadly speaking, image-order rendering is simpler to get working and more flexible in the effects that can be produced, and usually (though not always) takes much more execution time to produce a comparable image. 
图像顺序和对象顺序的渲染方法可以计算出完全相同的图像，但它们适用于计算不同类型的效果，并具有相当不同的性能特征。我们将在第8章中讨论了两者之后探讨它们的比较优势，但总体而言，图像顺序渲染更容易上手，在产生各种效果方面更加灵活，通常（尽管不总是）需要更多的执行时间来生成一个可比的图像。

> In a ray tracer, it is easy to compute accurate shadows and reflections, which are awkward in the object-order framework. 
> 在光线追踪器中，计算准确的阴影和反射较为容易，而在对象顺序框架中则显得复杂。

Ray tracing is an image-order algorithm for making renderings of 3D scenes, and we’ll consider it first because it’s possible to get a ray tracer working without developing any of the mathematical machinery that’s used for object-order rendering. 
光线追踪是一种用于制作三维场景渲染的图像顺序算法，我们首先考虑它，因为可以在不开发用于对象顺序渲染的数学机制的情况下使光线追踪器工作。

## 4.1 The Basic Ray-Tracing Algorithm 基本光线追踪算法

A ray tracer works by computing one pixel at a time, and for each pixel the basic task is to find the object that is seen at that pixel’s position in the image. Each pixel “looks” in a different direction, and any object that is seen by a pixel must intersect the viewing ray, a line that emanates from the viewpoint in the direction that pixel is looking. The particular object we want is the one that intersects the viewing ray nearest the camera, since it blocks the view of any other objects behind it. Once that object is found, a shading computation uses the intersection point, surface normal, and other information (depending on the desired type of rendering) to determine the color of the pixel. This is shown in Figure 4.1, where the ray intersects two triangles, but only the first triangle hit, $T_2$, is shaded. A basic ray tracer therefore has three parts: 
光线追踪器的工作原理是一次计算一个像素，对于每个像素，基本任务是找到在图像中该像素位置看到的物体。 每个像素“看”的方向不同，并且像素所看到的任何对象都必须与视线相交，视线是从视点沿像素所看的方向发出的线。 我们想要的特定对象是与最接近相机的视线相交的对象，因为它阻挡了其后面的任何其他对象的视图。 一旦找到该对象，着色计算就会使用交点、表面法线和其他信息（取决于所需的渲染类型）来确定像素的颜色。 如图 4.1 所示，其中光线与两个三角形相交，但只有第一个三角形 $T_2$ 被着色。 因此，基本的光线追踪器由三个部分组成：
<img src=".\Images\Figure 4.1.png" alt="Figure 4.1" style="zoom:50%;" />
Figure 4.1. The ray is “traced” into the scene and the first object hit is the one seen through the pixel. In this case, the triangle $T_2$ is returned. 
图 4.1  光线被“追踪”到场景中，第一个击中的物体是通过像素看到的物体。 在本例中，返回三角形 $T_2$。

A basic ray tracer therefore has three parts: ·
因此，基本的光线追踪器由三个部分组成：

1. ray generation, which computes the origin and direction of each pixel’s viewing ray based on the camera geometry;
   光线生成，根据相机几何图形计算**每个像素观看光线的原点和方向**;
2. ray intersection, which finds the closest object intersecting the viewing ray;
   光线相交，寻找与观察光线相交的最近的物体;
3. shading, which computes the pixel color based on the results of ray intersection. 
   着色，基于光线相交的结果计算像素颜色。

The structure of the basic ray tracing program is: 
基本光线追踪程序的结构是:

```lua
for each pixel do
	compute viewing ray
	find first object hit by ray and its surface normal n
	set pixel color to value computed from hit point, light, and n
对于每个像素
    计算观察射线
    求第一个被射线击中的物体及其表面法向n
    将像素颜色设置为根据命中点、光线和n计算的值
```

This chapter covers basic methods for ray generation, ray intersection, and shading, that are sufficient for implementing a simple demonstration ray tracer. For a really useful system, more efficient ray intersection techniques from Chapter 12 need to be added, and the real potential of a ray tracer will be seen with the more advanced shading methods from Chapter 10 and the additional rendering techniques from Chapter 13. 
本章涵盖了光线生成、光线相交和着色的基本方法，足以实现一个简单的演示光线追踪器。然而，若欲打造一款真正实用的系统，则需要引入第12章更高效的光线相交技术。而真正展现光线追踪器的潜力，则体现在第10章更先进的着色方法以及第13章的附加渲染技术。

 

## 4.2 Perspective 透视

The problem of representing a 3D object or scene with a 2D drawing or painting was studied by artists hundreds of years before computers. Photographs also represent 3D scenes with 2D images. While there are many unconventional ways to make images, from cubist painting to fisheye lenses (Figure 4.2) to peripheral cameras, the standard approach for both art and photography, as well as computer graphics, is linear perspective, in which 3D objects are projected onto an image plane in such a way that straight lines in the scene become straight lines in the image. 
艺术家在计算机问世数百年前就已开始研究用二维的绘画或素描来表现三维物体或场景的问题。而照片同样以二维图像呈现三维场景。尽管创作图像的方法多种多样，从立体主义绘画到鱼眼镜头（见图4.2）再到周边摄像机，但在艺术、摄影以及计算机图形学中，一直以来的标准方法都是线性透视。这种透视方法中，三维物体被投影到图像平面上，使得场景中的直线在图像中保持为直线。
<img src=".\Images\Figure 4.2.png" alt="Figure 4.2" style="zoom:67%;" />
Figure 4.2. An image taken with a fisheye lens is not a linear perspective image. Photo courtesy Philip Greenspun. 
图4.2 用鱼眼镜头拍摄的图像不是线性透视图像。图片由Philip Greenspun提供。

The simplest type of projection is parallel projection, in which 3D points are mapped to 2D by moving them along a projection direction until they hit the image plane (Figures 4.3–4.4). The view that is produced is determined by the choice of projection direction and image plane. If the image plane is perpendicular  to the view direction, the projection is called orthographic; otherwise it is called oblique. 
最简单的投影类型是平行投影，其中3D点通过沿投影方向移动，直至碰到图像平面而映射为2D图像（见图4.3-4.4）。所得的视图由投影方向和图像平面的选择决定。若图像平面与视角方向垂直，则称为正交投影；否则称为斜投影。这一选择影响着最终呈现的视觉效果，是一种在视觉艺术和计算机图形学中常用的基础技术。
<img src=".\Images\Figure 4.3.png" alt="Figure 4.3" style="zoom:80%;" />
Figure 4.3. When projection lines are parallel and perpendicular to the image plane, the resulting views are called orthographic. 
图 4.3  当**投影线平行和垂直于图像平面**时，所得视图称为**正交视图**。
<img src="Images\Figure 4.4.png" alt="Figure 4.4" style="zoom:80%;" />
Figure 4.4. A parallel projection that has the image plane at an angle to the projection direction is called oblique (right). In perspective projection, the projection lines all pass through the viewpoint, rather than being parallel (left). The illustrated perspective view is non-oblique because a projection line drawn through the center of the image would be perpendicular to the image plane.
图 4.4  像**平面与投影方向成一定角度的平行投影称为斜投影**（右边的投影）。在透视投影中，投影线全部穿过视点，而不是平行（左边的投影）。所示透视图是非倾斜的，因为穿过图像中心绘制的投影线将垂直于图像平面。

Parallel projections are often used for mechanical and architectural drawings because they keep parallel lines parallel and they preserve the size and shape of planar objects that are parallel to the image plane. 
平行投影通常用于机械和建筑绘图，因为它们使平行线保持平行，并保持与图像平面平行的平面物体的大小和形状。

> Some books reserve “orthographic” for projection directions that are parallel to the coordinate axes. 
> 有些书籍将“正交投影”一词保留给与坐标轴平行的投影方向。

The advantages of parallel projection are also its limitations. In our everyday experience (and even more so in photographs) objects look smaller as they get farther away, and as a result parallel lines receding into the distance do not appear parallel. This is because eyes and cameras don’t collect light from a single viewing direction; they collect light that passes through a particular viewpoint. As has been recognized by artists since the Renaissance, we can produce natural-looking views using perspective projection: we simply project along lines that pass through a single point, the viewpoint, rather than along parallel lines (Figure 4.4). In this way, objects farther from the viewpoint naturally become smaller when they are projected. A perspective view is determined by the choice of viewpoint (rather than projection direction) and image plane. As with parallel views, there are oblique and non-oblique perspective views; the distinction is made based on the projection direction at the center of the image.
平行投影的优势同时也是其局限所在。在我们日常的经验中（甚至在照片中更为明显），随着物体远离观察者，它们看起来越来越小，导致远处的平行线在投影中不再呈平行状态。这是因为眼睛和相机不是从单一的视角收集光线，而是通过特定的观察点收集光线。正如自文艺复兴时期以来艺术家所认识到的那样，我们可以通过透视投影来产生自然的视觉效果：我们只需沿着通过一个单一点（即观察点）的线进行投影，而不是沿着平行线（见图4.4）。这样，远离观察点的物体在投影时自然而然地变小。透视视图的形成由观察点的选择（而非投影方向）和图像平面决定。与平行视图一样，透视视图可分为斜投影和非斜投影，这一区别基于图像中心的投影方向。

You may have learned about the artistic conventions of three-point perspective, a system for manually constructing perspective views (Figure 4.5). A surprising fact about perspective is that all the rules of perspective drawing will be followed automatically if we follow the simple mathematical rule underlying perspective: objects are projected directly toward the eye, and they are drawn where they meet a view plane in front of the eye.
或许你已经了解过三点透视法的艺术惯例，这是一种手工构建透视视图的系统（见图4.5）。关于透视的一个令人惊讶的事实是，如果我们遵循透视的简单数学规则，即物体直接朝向眼睛投影，并在眼前的视平面上绘制它们相交的位置，那么透视绘图的所有规则将会自动得到遵循。
<img src=".\Images\Figure 4.5.png" alt="Figure 4.5" style="zoom:67%;" />
Figure 4.5. In three-point perspective, an artist picks “vanishing points” where parallel lines meet. Parallel horizontal lines will meet at a point on the horizon. Every set of parallel lines has its own vanishing points. These rules are followed automatically if we implement perspective based on the correct geometric principles. 
图4.5 在三点透视法中，艺术家选择平行线相交的“消失点”。平行的水平线会在地平线上的一点相交。每一组平行线都有自己的消失点。如果我们基于正确的几何原理实现透视图，就会自动遵循这些规则。

## 4.3 Computing Viewing Rays  计算观察光线

From the previous section, the basic tools of ray generation are the viewpoint (or view direction, for parallel views) and the image plane. There are many ways to work out the details of camera geometry; in this section we explain one based on orthonormal bases that supports normal and oblique parallel and orthographic views. 
在前一节中，光线生成的基本工具是观察点（对于平行视图则是视角方向）和图像平面。有许多方法可以处理相机几何的细节；在这一节中，我们将解释一种基于正交基的方法，支持正交和斜交平行以及正交视图。

In order to generate rays, we first need a mathematical representation for a ray. A ray is really just an origin point and a propagation direction; a 3D parametric line is ideal for this. As discussed in Section 2.5.7, the 3D parametric line from the eye e to a point s on the image plane (Figure 4.6) is given by 
为了生成光线，我们首先需要一个光线的数学表示。光线实际上只是一个起源点和传播方向；一个三维参数化线非常适合这个目的。正如在第2.5.7节讨论的那样，从眼睛e到图像平面上的点s的三维参数化线（见图4.6）由下式给出
$\bold{p}(t) = \bold{e} + t(s - \bold{e})  $
![Figure 4.6](.\Images\Figure 4.6.png)
Figure 4.6. The ray from the eye to a point on the image plane. 
图 4.6 从眼睛到图像平面上的一点的光线

This should be interpreted as, “we advance from e along the vector $(\bold{s} - \bold{e})$ a fractional distance $t$ to find the point $\bold{p}$.” So given $t$, we can determine a point $\bold{p}$. The point $\bold{e}$ is the ray’s origin, and $\bold{s} - \bold{e}$ is the ray’s direction. 
这应该被解释为，“我们从 e 沿着向量 $(\bold{s} - \bold{e})$ 前进一小部分距离 $t$ 来找到点 $\bold{p}$。” 因此给定$t$，我们可以确定一个点$\bold{p}$。 点 $\bold{e}$ 是射线的原点，$\bold{s} - \bold{e}$ 是射线的方向。

Note that $\bold{p}(0) = \bold{e}$, and $\bold{p}(1) = \bold{s}$, and more generally, if $0 < t_1 < t_2$, then $\bold{p}(t_1)$ is closer to the eye than $\bold{p}(t_2)$. Also, if $t < 0$, then $\bold{p}(t)$ is “behind” the eye. These facts will be useful when we search for the closest object hit by the ray that is not behind the eye. 
请注意，$\bold{p}(0) = \bold{e}$，$\bold{p}(1) = \bold{s}$，更一般地，如果$0 < t_1 < t_2$，那么$\bold{p}(t_1)$比$\bold{p}(t_2)$更靠近眼睛。此外，如果$t < 0$，那么$\bold{p}(t)$位于眼睛的“后方”。这些事实在我们寻找射线击中的最近物体时将会很有用，尤其是那些在眼睛前面的物体。

> Caution: we are overloading the variable $t$, which is the ray parameter and also the v-coordinate of the top edge of the image. 
> 注意：我们正在对变量$t$进行重载，它既是射线参数，也是图像顶部边缘的v坐标。

To compute a viewing ray, we need to know $\bold{e}$ (which is given) and $\bold{s}$. Finding $\bold{s}$ may seem difficult, but it is actually straightforward if we look at the problem in the right coordinate system. 
为了计算视线，我们需要知道 $\bold{e}$ （已给出）和 $\bold{s}$。 找到$\bold{s}$可能看起来很困难，但如果我们在正确的坐标系中看问题，实际上很简单。

All of our ray-generation methods start from an orthonormal coordinate frame known as the camera frame, which we’ll denote by $\bold{e}$, for the eye point, or viewpoint, and $\bold{u}$, $\bold{v}$, and $\bold{w}$ for the three basis vectors, organized with $\bold{u}$ pointing rightward (from the camera’s view), $\bold{v}$ pointing upward, and $\bold{w}$ pointing backward, so that {$\bold{u}$, $\bold{v}$, $\bold{w}$} forms a right-handed coordinate system. The most common way  to construct the camera frame is from the viewpoint, which becomes $\bold{e}$, the view  direction, which is $-\bold{w}$, and the up vector, which is used to construct a basis that has $\bold{v}$ and $\bold{w}$ in the plane defined by the view direction and the up direction, using  the process for constructing an orthonormal basis from two vectors described in Section 2.4.7. 
我们所有的光线生成方法都始于一个正交坐标框架，被称为相机坐标系，我们用$\bold{e}$表示眼睛点或观察点，$\bold{u}$、$\bold{v}$和$\bold{w}$表示三个基向量。这些基向量按照{$\bold{u}$，$\bold{v}$，$\bold{w}$}的顺序组织，其中$\bold{u}$指向右侧（从相机的视角），$\bold{v}$指向上方，$\bold{w}$指向背后，使得{$\bold{u}$，$\bold{v}$，$\bold{w}$}形成一个右手坐标系。构建相机坐标系的最常见方法是从观察点开始，观察点成为$\bold{e}$，视线方向为$-\bold{w}$，上向量用于构建一个基，该基在由视线方向和上方向定义的平面上包含$\bold{v}$和$\bold{w}$，使用构建正交基的过程，该过程在第2.4.7节中描述了从两个向量构建正交基的方法。
<img src=".\Images\Figure 4.7.png" alt="Figure 4.7" style="zoom:67%;" />
Figure 4.7. The sample points on the screen are mapped to a similar array on the 3D window. A viewing ray is sent to each of these locations. 
图4.7。屏幕上的采样点被映射到3D窗口上的相似数组中。每个这些位置都发送一条视线。

![Figure 4.8](.\Images\Figure 4.8.png)
Figure 4.8. The vectors of the camera frame, together with the view direction and up direction. The $\bold{w}$ vector is opposite the view direction, and the $\bold{v}$ vector is coplanar with $\bold{w}$ and the up vector. 
图4.8。相机坐标系的向量，以及视线方向和上方向。$\bold{w}$向量与视线方向相反，而$\bold{v}$向量与$\bold{w}$和上向量在同一平面上。

> Since $\bold{v}$ and $\bold{w}$ have to be perpendicular, the up vector and $\bold{v}$ are not generally the same. But setting the up vector to point straight upward in the scene will orient the camera in the way we would think of as “upright.” 
> 由于$\bold{v}$和$\bold{w}$必须垂直，上向量和$\bold{v}$通常不相同。但是，将上向量设置为在场景中指向直上将使相机朝向我们所认为的“站立的”方向。

### 4.3.1 Orthographic Views 正交视图

For an orthographic view, all the rays will have the direction $-\bold{w}$. Even though a parallel view doesn’t have a viewpoint per se, we can still use the origin of the  camera frame to define the plane where the rays start, so that it’s possible for objects to be behind the camera. 
对于正交视图，所有的光线都将具有$-\bold{w}$的方向。尽管平行视图本身没有固定的观察点，我们仍然可以使用相机坐标系的原点来定义光线起始的平面，从而使物体有可能位于相机的背后。

The viewing rays should start on the plane defined by the point $\bold{e}$ and the vectors $\bold{u}$ and $\bold{v}$; the only remaining information required is where on the plane the image is supposed to be. We’ll define the image dimensions with four numbers, for the four sides of the image: $l$ and $r$ are the positions of the left and right edges of the image, as measured from $\bold{e}$ along the $\bold{u}$ direction; and $b$ and $t$ are the positions of the bottom and top edges of the image, as measured from $\bold{e}$ along the $\bold{v}$ direction. Usually $l < 0 < r$ and $b < 0 < t$. (See Figure 4.9.) 
视线应该起始于由点$\bold{e}$和向量$\bold{u}$、$\bold{v}$定义的平面上；唯一缺失的信息是图像应该在平面上的哪个位置。我们将用四个数字定义图像的尺寸，分别对应图像的四边：$l$和$r$分别表示图像的左边和右边的位置，以$\bold{e}$沿着$\bold{u}$方向测量；而$b$和$t$分别表示图像的底边和顶边的位置，以$\bold{e}$沿着$\bold{v}$方向测量。通常情况下，$l < 0 < r$ 以及 $b < 0 < t$。（见图4.9。）
![Figure 4.9](.\Images\Figure 4.9.png)
Figure 4.9. Ray generation using the camera frame. Left: In an orthographic view, the rays start at the pixels’ locations on the image plane, and all share the same direction, which is equal to the view direction. Right: In a perspective view, the rays start at the viewpoint, and each ray’s direction is defined by the line through the viewpoint, $\bold{e}$, and the pixel’s location on the image plane. 
图4.9。使用相机坐标系进行光线生成。左图：在正交视图中，光线起始于图像平面上像素的位置，且所有光线具有相同的方向，即与视线方向相同。右图：在透视视图中，光线起始于观察点，每条光线的方向由通过观察点$\bold{e}$和图像平面上像素位置的直线定义。

> It might seem logical that orthographic viewing rays should start from infinitely far away, but then it would not be possible to make orthographic views of an object inside a room, for instance 
> 或许从无穷远处开始的正交视线似乎是合乎逻辑的，但这样的话就无法制作室内物体的正交视图了，比如一个房间内的物体。

> Many systems assume that $l = – r$ and $b = – t$ so that a width and a height suffice.
> 许多系统假设 $l = – r$ 和 $b = – t$ 这样宽度和高度就足够了

In Section 3.2 we discussed pixel coordinates in an image. To fit an image with $n_x × n_y$ pixels into a rectangle of size $(r - l) \cross (t - b)$, the pixels are spaced a distance $(r - l)/n_x$ apart horizontally and $(t - b)/n_y$ apart vertically, with a half-pixel space around the edge to center the pixel grid within the image rectangle. This means that the pixel at position $(i, j)$ in the raster image has the position
在第3.2节中，我们讨论了图像中的像素坐标。为了将一个包含$n_x × n_y$像素的图像适配到尺寸为$(r - l) \cross (t - b)$的矩形中，水平间隔为$(r - l)/n_x$，垂直间隔为$(t - b)/n_y$，在图像矩形边缘周围有半个像素的空间以将像素网格置于图像矩形的中心位置。这意味着光栅图像中位置为$(i, j)$的像素的位置是：
$$
u = l + (r − l)(i + 0.5)/n_x, \\
v = b + (t − b)(j + 0.5)/n_y, \\
(4.1)
$$
where $(u, v)$ are the coordinates of the pixel’s position on the image plane, measured with respect to the origin $\bold{e}$ and the basis $\{\bold{u}, \bold{v}\}$. 
其中，$(u, v)$ 是像素在图像平面上的坐标，相对于原点 $\bold{e}$ 和基底 ${\bold{u}, \bold{v}}$ 来测量。

In an orthographic view, we can simply use the pixel’s image-plane position as the ray’s starting point, and we already know the ray’s direction is the view direction. The procedure for generating orthographic viewing rays is then: 
在正交视图中，我们可以简单地使用像素的图像平面位置作为射线的起点，并且我们已经知道射线的方向就是视图方向。 生成正交观察光线的过程是：

$compute\ u\ and\ v\ using\ (4.1) \\
ray.direction ← -\bold{w} \\
ray.origin ← \bold{e} + u\bold{u} + v\bold{v} \\ $

> With $l$ and $r$ both specified, there is redundancy: moving the viewpoint a bit to the right and correspondingly decreasing $l$ and $r$ will not change the view (and similarly on the $\bold{v}$-axis) 
> 当$l$和$r$都已指定时，存在冗余：稍微将观察点向右移动，并相应减小$l$和$r$将不会改变视图（在$\bold{v}$轴上同样如此）。

It’s very simple to make an oblique parallel view: just allow the image plane normal w to be specified separately from the view direction $\bold{d}$. The procedure is then exactly the same, but with $\bold{d}$ substituted for $-\bold{w}$. Of course $\bold{w}$ is still used to construct $\bold{u}$ and $\bold{v}$. 
制作斜交平行视图非常简单：只需允许图像平面法线$\bold{w}$与视线方向$\bold{d}$分别指定。然后，程序完全相同，只是用$\bold{d}$代替$-\bold{w}$。当然，$\bold{w}$仍然用于构建$\bold{u}$和$\bold{v}$。

### 4.3.2 Perspective Views 透视视图

For a perspective view, all the rays have the same origin, at the viewpoint; it is the directions that are different for each pixel. The image plane is no longer positioned at $\bold{e}$, but rather some distance $d$ in front of $\bold{e}$; this distance is the image plane distance, often loosely called the focal length, because choosing $d$ plays the same role as choosing focal length in a real camera. The direction of each ray is defined by the viewpoint and the position of the pixel on the image plane. This situation is illustrated in Figure 4.9, and the resulting procedure is similar to the  orthographic one:
透视视图中，所有光线都源自观察点；不同的是各像素的方向。图像平面不再位于$\bold{e}$处，而是在$\bold{e}$前方一段距离$d$处；这个距离称为图像平面距离，通常宽松地称为焦距，因为选择$d$的作用类似于在真实相机中选择焦距。每条光线的方向由观察点和图像平面上像素的位置定义。这种情况在图4.9中有所说明，生成的过程与正交视图类似：
$compute\ u\ and\ v\ using\ (4.1) \\
ray.direction ← -d \bold{w} + u \bold{u} + v \bold{v} \\
ray.origin ← \bold{e}$

As with parallel projection, oblique perspective views can be achieved by specifying the image plane normal separately from the projection direction, then replacing $-d\bold{w}$ with $d\bold{d}$ in the expression for the ray direction. 
与平行投影一样，可以通过指定与投影方向分开的图像平面法线，然后将光线方向表达式中的 $-d\bold{w}$ 替换为 $d\bold{d}$ 来获得倾斜透视图 。

## 4.4 Ray-Object Intersection 射线-物体相交

Once we’ve generated a ray $\bold{e}+ t\bold{d}$, we next need to find the first intersection with any object where $t > 0$. In practice, it turns out to be useful to solve a slightly more general problem: find the first intersection between the ray and a surface that occurs at a $t$ in the interval $[t_0, t_1]$. The basic ray intersection is the case where $t_0 = 0$ and $t_1 = +∞$. We solve this problem for both spheres and triangles. In the next section, multiple objects are discussed. 
生成了射线$\bold{e}+ t\bold{d}$后，接下来我们需要寻找与任何物体的首次相交，其中$t > 0$。在实践中，解决一个略微更一般的问题会变得更为实用：找到射线与表面的首次交点，该交点发生在区间$[t_0, t_1]$内的$t$。基本的射线相交是$t_0 = 0$且$t_1 = +∞$的情况。我们为球体和三角形都解决了这个问题。在下一部分中，将讨论多个对象的情况。

### 4.4.1 Ray-Sphere Intersection   射线-球体相交

Given a ray $\bold{p}(t) = \bold{e} + t\bold{d}$ and an implicit surface $f(\bold{p}) = 0$ (see Section 2.5.3), we’d like to know where they intersect. Intersection points occur when points on the ray satisfy the implicit equation, so the values of $t$ we seek are those that solve the equation
考虑一条射线$\bold{p}(t) = \bold{e} + t\bold{d}$和一个隐式表面$f(\bold{p}) = 0$（详见第2.5.3节），我们希望知道它们在何处相交。相交点发生在射线上的点满足隐式方程的情况下，因此我们寻找的$t$值是解该方程的值
$f(\bold{p}(t)) = 0\ or\ f(\bold{e} + t\bold{d}) = 0  $

A sphere with center $\bold{c} = (x_c, y_c, z_c)$ and radius R can be represented by the implicit equation
中心为 $\bold{c} = (x_c, y_c, z_c)$ 且半径为 R 的球体可以用隐式方程表示
$(x - x_c)^2 + (y - y_c)^2 + (z - z_c)^2 - R^2 = 0.  $

We can write this same equation in vector form: 
我们可以将同样的方程写成向量形式：
$(\bold{p} - \bold{c}) · (\bold{p} - \bold{c}) - R^2 = 0.  $

Any point $\bold{p}$ that satisfies this equation is on the sphere. If we plug points on the ray $\bold{p}(t) = \bold{e} + t\bold{d}$ into this equation, we get an equation in terms of t that is satisfied by the values of $t$ that yield points on the sphere:
满足该方程的任何点 $\bold{p}$ 都在球体上。 如果我们将射线 $\bold{p}(t) = \bold{e} + t\bold{d}$ 上的点代入这个方程，我们就得到一个以 t 表示的方程，它满足$t$的值在球体上产生点：
$(\bold{e} + t\bold{d}- \bold{c}) · (\bold{e} + t\bold{d} - \bold{c}) - R^2 = 0.  $

Rearranging terms yields
重新排列
$(\bold{d} · \bold{d})t^2 + 2\bold{d} · (\bold{e} - \bold{c})t + (\bold{e} - \bold{c}) · (\bold{e} - \bold{c}) - R^2 = 0.  $

Here, everything is known except the parameter $t$, so this is a classic quadratic equation in $t$, meaning it has the form
这里，除了参数$t$，其他都是已知的，所以这是$t$的经典二次方程，也就是说它有这样的形式
$At^2 + Bt + C = 0  $

The solution to this equation is discussed in Section 2.2. The term under the square root sign in the quadratic solution, $B^2 - 4AC$, is called the discriminant and tells us how many real solutions there are. If the discriminant is negative, its square root is imaginary and the line and sphere do not intersect. If the discriminant is positive, there are two solutions: one solution where the ray enters the sphere and one where it leaves. If the discriminant is zero, the ray grazes the sphere, touching it at exactly one point. Plugging in the actual terms for the sphere and canceling a factor of two, we get 
这个方程的解讨论在第2.2节中。在二次方程的解中，位于平方根符号下的表达式$B^2 - 4AC$被称为判别式，它告诉我们有多少个实数解。如果判别式为负，其平方根为虚数，表示直线与球体不相交。如果判别式为正，有两个解：一个解表示射线进入球体，另一个解表示射线离开球体。如果判别式为零，射线与球体相切，恰好在一个点上接触。将实际的球体术语代入并约去一个因子二，我们得到
$t = \frac{-\bold{d} · (\bold{e} - \bold{c}) ±  \sqrt{(\bold{d} · (\bold{e} - \bold{c}))^2 - (\bold{d} · \bold{d}) ((\bold{e} - \bold{c}) · (\bold{e} - \bold{c}) - R^2)  }}{(\bold{d} · \bold{d})}\\$

In an actual implementation, you should first check the value of the discriminant before computing other terms. If the sphere is used only as a bounding object for more complex objects, then we need only determine whether we hit it; checking the discriminant suffices. 
在实际实现中，您应该在计算其他项之前首先检查判别式的值。 如果球体仅用作更复杂物体的边界物体，那么我们只需要确定是否击中它即可； 检查判别式就足够了。

As discussed in Section 2.5.4, the normal vector at point $\bold{p}$ is given by the gradient $\bold{n} = 2(\bold{p} - \bold{c})$. The unit normal is $(\bold{p} - \bold{c})/R$. 
正如第2.5.4节所讨论的，点$\bold{p}$处的法向量由梯度给出，即$\bold{n} = 2(\bold{p} - \bold{c})$。单位法向量为$(\bold{p} - \bold{c})/R$。

### 4.4.2 Ray-Triangle Intersection 射线-三角形相交

There are many algorithms for computing ray-triangle intersections. We will present the form that uses barycentric coordinates for the parametric plane containing the triangle, because it requires no long-term storage other than the vertices of the triangle (Snyder & Barr, 1987). 
计算光线与三角形相交的算法有很多种。我们将介绍一种采用重心坐标表示法的形式，用于参数化包含该三角形的平面，因为这种方法除了三角形的顶点之外，不需要长期存储其他信息（Snyder＆Barr，1987）。

To intersect a ray with a parametric surface, we set up a system of equations where the Cartesian coordinates all match: 
为了使射线与参数曲面相交，我们建立了一个方程组，其中笛卡尔坐标都是匹配的:
$$
\begin{rcases}
x_e + tx_d = f(u, v) \\
y_e + ty_d = g(u, v) \\
z_e + tz_d = h(u, v)
\end{rcases}
or, \bold{e} + t\bold{d} = \bold{f}(u, v).
$$
Here, we have three equations and three unknowns ($t$, $u$, and $v$), so we can solve numerically for the unknowns. If we are lucky, we can solve for them analytically.
在这里，我们有三个方程和三个未知数（$t$、$u$ 和 $v$），因此我们可以对未知数进行数值求解。 如果幸运的话，我们可以通过分析来解决它们。

In the case where the parametric surface is a parametric plane, the parametric equation can be written in vector form as discussed in Section 2.7.2. If the vertices of the triangle are $\bold{a}$, $\bold{b}$, and $\bold{c}$, then the intersection will occur when
在参数曲面是参数平面的情况下，参数方程可以写成矢量形式，如第 2.7.2 节所述。 如果三角形的顶点是 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$，则交集将发生在
$$
\bold{e} + t\bold{d} = \bold{a} + β(\bold{b} − \bold{a}) + γ(\bold{c} − \bold{a}), (4.2)
$$
for some $t$, $β$, and $γ$. The intersection $\bold{p}$ will be at $\bold{e} + t\bold{d}$ as shown in Figure 4.10. Again, from Section 2.7.2, we know the intersection is inside the triangle if and only if $β > 0$, $γ > 0$, and $β + γ < 1$. Otherwise, the ray has hit the plane outside the triangle, so it misses the triangle. If there are no solutions, either the triangle is degenerate or the ray is parallel to the plane containing the triangle. 
对于某些$t$、$β$和$γ$。如图4.10所示，交点$\bold{p}$将位于$\bold{e} + t\bold{d}$。再次从第2.7.2节得知，仅当$β > 0$，$γ > 0$且$β + γ < 1$时，交点在三角形内。否则，光线击中了三角形外部的平面，因此未与三角形相交。如果没有解，要么三角形是退化的，要么光线与包含三角形的平面平行。
![Figure 4.10](.\Images\Figure 4.10.png)
Figure 4.10. The ray hits the plane containing the triangle at point $\bold{p}$
图4.10 射线在点$\bold{p}$处击中包含三角形的平面

To solve for $t$, $β$, and $γ$ in Equation (4.2), we expand it from its vector form into the three equations for the three coordinates: 
为了求解方程 (4.2) 中的 $t$、$β$ 和 $γ$，我们将其从向量形式展开为三个坐标的三个方程：
$x_e + tx_d = x_a + β(x_b - x_a) + γ(x_c - x_a), \\
y_e + ty_d = y_a + β(y_b - y_a) + γ(y_c - y_a), \\
z_e + tz_d = z_a + β(z_b - z_a) + γ(z_c - z_a).  $

This can be rewritten as a standard linear system: 
这可以重写为一个标准的线性系统:
$$
\begin{bmatrix}
x_a − x_b & x_a − x_c & x_d \\
y_a − y_b & y_a − y_c & y_d \\
z_a − z_b & z_a − z_c & z_d
\end{bmatrix}
\begin{bmatrix}
β \\
γ \\
t
\end{bmatrix}
 = \begin{bmatrix}
x_a − x_e \\
y_a − y_e \\
z_a − z_e
\end{bmatrix}
$$
The fastest classic method to solve this 3 × 3 linear system is Cramer’s rule. This gives us the solutions 
解决这个3 × 3线性系统的最快经典方法是克莱默法则。 这给了我们解决方案
$$
β = \frac{\begin{vmatrix}
x_a − x_e & x_a − x_c & x_d \\
y_a − y_e & y_a − y_c & y_d \\
z_a − z_e & z_a − z_c & z_d
\end{vmatrix}} {|\bold{A}|} \\

γ = \frac{\begin{vmatrix}
x_a − x_b & x_a − x_e & x_d \\
y_a − y_b & y_a − y_e & y_d \\
z_a − z_b & z_a − z_e & z_d
\end{vmatrix}} {|\bold{A}|} \\

t = \frac{\begin{vmatrix}
x_a − x_b & x_a − x_c & x_a − x_e \\
y_a − y_b & y_a − y_c & y_a − y_e \\ 
z_a − z_b & z_a − z_c & z_a − z_e
\end{vmatrix}} {|\bold{A}|} \\
$$
where the matrix $\bold{A}$ is
其中矩阵 $\bold{A}$ 是
$$
\bold{A} = \begin{bmatrix}
x_a - x_b & x_a - x_c & x_d \\
y_a - y_b & y_a - y_c & y_d \\
z_a - z_b & z_a - z_c & z_d
\end{bmatrix}
$$
and $|\bold{A}|$ denotes the determinant of $\bold{A}$. The 3×3 determinants have common sub-terms that can be exploited. Looking at the linear systems with dummy variables 
$|\bold{A}|$ 表示 $\bold{A}$ 的行列式。 3×3 行列式有可以利用的共同子项。 查看具有虚拟变量的线性系统
$$
\begin{bmatrix}
a & d & g \\
b & e & h \\
c & f & i
\end{bmatrix}
\begin{bmatrix}
β \\
γ \\
t
\end{bmatrix}
= \begin{bmatrix}
j \\
k \\
l
\end{bmatrix}
$$
Cramer’s rule gives us 
克莱默法则给了我们
$$
β = \frac{j(ei − hf) + k(gf − di) + l(dh − eg)}{M} \\
γ = \frac{i(ak − jb) + h(jc − al) + g(bl − kc)}{M} \\
β = \frac{f(ak − jb) + e(jc − al) + d(bl − kc)}{M} \\ 
\\
M = a(ei − hf) + b(gf − di) + c(dh − eg)
$$
We can reduce the number of operations by reusing numbers such as “ei-minus-hf.”
我们可以通过重复使用诸如“ei-minus-hf”等数字来减少操作次数。

The algorithm for the ray-triangle intersection for which we need the linear solution can have some conditions for early termination. Thus, the function should look something like: 
我们需要线性解的射线与三角形相交的算法可以有一些提前终止的条件。 因此，该函数应该类似于：

```python
boolean raytri (ray r, vector3 a, vector3 b, vector3 c, interval [t0, t1])
    compute t
    if (t < t0) or (t > t1) then
    	return false
    
    compute γ
    if (γ < 0) or (γ > 1) then
    	return false
    
    compute β
    if (β < 0) or (β > 1 − γ) then
    	return false
    
    return true
```

### 4.4.3 Ray-Polygon Intersection 射线与多边形相交

Given a planar polygon with m vertices $\bold{p}_1$ through $\bold{p}_m$ and surface normal $\bold{n}$, we first compute the intersection points between the ray $\bold{e} + t\bold{d}$ and the plane containing the polygon with implicit equation
给定一个具有 m 个顶点 $\bold{p}_1$ 到 $\bold{p}_m$ 和表面法线 $\bold{n}$ 的平面多边形，我们首先计算光线 $\bold{e}  + t\bold{d}$ 之间的交点和包含具有隐式方程的多边形的平面
$(\bold{p} - \bold{p}_1) · \bold{n} = 0.  $

We do this by setting $\bold{p} = \bold{e} + t\bold{d}$ and solving for $t$ to get
我们通过设置 $\bold{p} = \bold{e} + t\bold{d}$ 并求解 $t$ 得到
$t = \frac{(\bold{p}_1 - \bold{e}) · \bold{n}  } {\bold{d} · \bold{n}  } \\$

This allows us to compute $\bold{p}$. If $\bold{p}$ is inside the polygon, then the ray hits it; otherwise, it does not.
这使我们能够计算$\bold{p}$。 如果 $\bold{p}$ 在多边形内部，则光线击中它； 否则，它不会。

We can answer the question of whether $\bold{p}$ is inside the polygon by projecting the point and polygon vertices to the $xy$ plane and answering it there. The easiest way to do this is to send any 2D ray out from $\bold{p}$ and to count the number of intersections between that ray and the boundary of the polygon (Sutherland, Sproull, & Schumacker, 1974; Glassner, 1989). If the number of intersections is odd, then the point is inside the polygon; otherwise it is not. This is true because a ray that goes in must go out, thus creating a pair of intersections. Only a ray that starts inside will not create such a pair. To make computation simple, the 2D ray may as well propagate along the x-axis: 
我们可以通过将点和多边形顶点投影到 $xy$ 平面并在那里回答来回答 $\bold{p}$ 是否在多边形内部的问题。 最简单的方法是从 $\bold{p}$ 发出任何 2D 射线，并计算该射线与多边形边界之间的交点数量 (Sutherland, Sproull, & Schumacker, 1974; Glassner, 1989 ）。 如果交点的数量是奇数，则该点在多边形内部； 否则就不是。 这是正确的，因为进入的光线必须出去，从而创建一对交叉点。 只有从内部开始的射线不会创建这样的射线对。 为了使计算简单，2D 射线也可以沿 x 轴传播：
$$
\begin{bmatrix}
x \\
y
\end{bmatrix}
 = \begin{bmatrix}
x_p \\
y_p
\end{bmatrix}
+ s\begin{bmatrix}
1 \\
0
\end{bmatrix}
$$
It is straightforward to compute the intersection of that ray with the edges such as $(x_1, y_1, x_2, y_2)$ for $s ∈ (0, ∞)$. 
计算该射线与边的交集很简单，例如 $(x_1, y_1, x_2, y_2)$ 对于 $s ∈ (0, ∞)$。

A problem arises, however, for polygons whose projection into the $xy$ plane is a line. To get around this, we can choose among the $xy$, $yz$, or $zx$ planes for whichever is best. If we implement our points to allow an indexing operation, e.g., $\bold{p}(0) = x_p$ then this can be accomplished as follows:  
然而，对于在 $xy$ 平面上的投影是一条线的多边形，就会出现问题。 为了解决这个问题，我们可以在 $xy$、$yz$ 或 $zx$ 平面中选择最好的一个。 如果我们实现我们的点以允许索引操作，例如 $\bold{p}(0) = x_p$ 则可以按如下方式完成：

```python
if (abs(zn) > abs(xn)) and (abs(zn) > abs(yn)) then
	index0 = 0
	index1 = 1
else if (abs(yn) > abs (xn)) then
	index0 = 0
	index1 = 2
else
	index0 = 1
	index1 = 2
```

Now, all computations can use $\bold{p}$(index0) rather than $x_p$, and so on. 
现在，所有的计算都可以使用$\bold{p}$(index0)而不是$x_p$，以此类推。

Another approach to polygons, one that is often used in practice, is to replace them by several triangles.
另一种在实践中经常使用的多边形方法是将它们替换为多个三角形。

### 4.4.4 Intersecting a Group of Objects 射线与组对象相交

Of course, most interesting scenes consist of more than one object, and when we intersect a ray with the scene we must find only the closest intersection to the camera along the ray. A simple way to implement this is to think of a group of objects as itself being another type of object. To intersect a ray with a group, you simply intersect the ray with the objects in the group and return the intersection with the smallest $t$ value. The following code tests for hits in the interval $t ∈ [t_0, t_1]$: 
当然，最有趣的场景由多个对象组成，当我们将一条光线与场景相交时，我们必须只找到沿光线与相机最近的交点。 实现这一点的一个简单方法是将一组对象本身视为另一种类型的对象。 要将射线与组相交，只需将射线与组中的对象相交并返回具有最小 $t$ 值的交集。 以下代码测试区间 $t ∈ [t_0, t_1]$ 中的命中：

```python
hit = false
for each object o in the group do
	if (o is hit at ray parameter t and t ∈ [t0, t1]) then
		hit = true
		hitobject = o
		t1 = t
return hit
```

![Figure 4.11](.\Images\Figure 4.11.png)
Figure 4.11. A simple scene rendered with only ray generation and surface intersection, but no shading; each pixel is just set to a fixed color depending on which object it hit. 
图 4.11  一个简单的场景，仅使用光线生成和表面相交进行渲染，但没有着色； 每个像素只是根据它击中的对象设置为固定颜色。

### ChatGPT

> 判断射线与球体是否相交通常涉及参数化表示法和代数几何的概念。以下是详细的步骤：
>
> 1. **射线参数化：** 射线可以用参数方程表示为 $ \bold{p}(t) = \bold{o} + t\bold{d} $，其中 $ \bold{o} $ 是射线的起点， $ \bold{d} $ 是射线的方向向量，而 $ t $ 是参数，可以是实数。
>
> 2. **球体方程：** 球体的方程通常为 $ (\bold{p} - \bold{c}) \cdot (\bold{p} - \bold{c}) = r^2 $，其中 $ \bold{c} $ 是球心的位置向量， $ r $ 是球的半径。
>
> 3. **代入射线方程：** 将射线方程代入球体方程，得到一个关于 $ t $ 的二次方程。具体而言，将射线方程中的 $ \bold{p} $ 替换为 $ \bold{o} + t\bold{d} $。方程形式为：
>    
>    $ ( \bold{o} + t\bold{d} - \bold{c}) \cdot (\bold{o} + t\bold{d} - \bold{c}) = r^2 $
>
>    这将导致一个形如 $ at^2 + bt + c = 0 $ 的二次方程，其中：
>
>    $ a = \bold{d} \cdot \bold{d} $,
>    $ b = 2(\bold{d} \cdot (\bold{o} - \bold{c})) $,
>    $ c = (\bold{o} - \bold{c}) \cdot (\bold{o} - \bold{c}) - r^2 $
>
> 4. **判别式：** 使用判别式 $ \Delta = b^2 - 4ac $ 来确定方程的解的性质。如果 $ \Delta < 0 $，则射线与球没有交点；如果 $ \Delta = 0 $，则射线与球相切于一个点；如果 $ \Delta > 0 $，则射线与球相交于两个点。
>
> 5. **解方程：** 如果存在相交点，通过解二次方程得到 $ t $ 的值。然后将这些值代入射线方程，可以找到相应的交点。
>
> 这样，通过这一系列步骤，你可以判断射线是否与给定的球体相交，并找到交点的位置。

> 判断射线与三角形是否相交是计算机图形学和计算几何中的常见问题。以下是详细的步骤：
>
> 1. **射线参数化：** 射线可以用参数方程表示为 $ \bold{p}(t) = \bold{o} + t\bold{d} $，其中 $ \bold{o} $ 是射线的起点， $ \bold{d} $ 是射线的方向向量，而 $ t $ 是参数，可以是实数。
>
> 2. **三角形的表示：** 三角形由三个顶点 $ \bold{v}_1, \bold{v}_2, \bold{v}_3 $ 组成。可以使用重心坐标系（barycentric coordinates）表示三角形内的点 $ \bold{p} $。重心坐标满足 $ \bold{p} = \beta\bold{v}_1 + \gamma\bold{v}_2 + (1-\beta-\gamma)\bold{v}_3 $，其中 $ \beta, \gamma $ 是重心坐标。
>
> 3. **射线与平面相交：** 将射线方程 $ \bold{p}(t) = \bold{o} + t\bold{d} $ 代入平面方程，可以得到一个关于 $ t $ 的表达式。平面方程通常表示为 $ \bold{n} \cdot (\bold{p} - \bold{v}_1) = 0 $，其中 $ \bold{n} $ 是三角形所在平面的法向量。
>
> 4. **求解重心坐标 $ \beta, \gamma $：** 利用射线与平面的交点，可以得到 $ t $ 的值。然后，通过将 $ \bold{p}(t) $ 代入重心坐标的表达式，求解 $ \beta, \gamma $。
>
> 5. **判断相交：** 如果 $ \beta, \gamma $ 满足 $ 0 \leq \beta \leq 1, 0 \leq \gamma \leq 1, \beta + \gamma \leq 1 $，则射线与三角形相交。这是因为在重心坐标系中，点 $ \bold{p} $ 在三角形内的条件为 $ 0 \leq \beta, \gamma \leq 1 $ 且 $ \beta + \gamma \leq 1 $。
>
> 6. **计算交点：** 如果相交，可以通过将 $ t $ 带入射线方程 $ \bold{p}(t) $ 计算实际的交点坐标。
>
> 通过这一系列步骤，你可以判断射线是否与给定的三角形相交，并找到交点的位置。





## 4.5 Shading  着色

Once the visible surface for a pixel is known, the pixel value is computed by evaluating a shading model. How this is done depends entirely on the application—methods range from very simple heuristics to elaborate numerical computations. In this chapter we describe the two most basic shading models; more advanced models are discussed in Chapter 10.
一旦确定了像素的可见表面，就通过评估一种着色模型来计算像素值。关于这一过程的具体实现，完全取决于应用的性质——方法从非常简单的经验法则到复杂的数值计算不等。在本章中，我们描述了两种最基本的着色模型；更高级的模型将在第十章进行探讨。

Most shading models, one way or another, are designed to capture the process of light reflection, whereby surfaces are illuminated by light sources and reflect part of the light to the camera. Simple shading models are defined in terms of illumination from a point light source. The important variables in light reflection are the light direction $\bold{l}$, which is a unit vector pointing toward the light source; the view direction $\bold{v}$, which is a unit vector pointing toward the eye or camera; the surface normal $\bold{n}$, which is a unit vector perpendicular to the surface at the point where reflection is taking place; and the characteristics of the surface—color, shininess, or other properties depending on the particular model. 
大多数着色模型在某种程度上都旨在捕捉光反射的过程，即表面受到光源照射并将部分光线反射给摄像机。简单的着色模型是基于来自点光源的照明定义的。在光反射中的重要变量包括光线方向 $\bold{l}$，它是指向光源的单位向量；视图方向 $\bold{v}$，它是指向眼睛或摄像机的单位向量；表面法线 $\bold{n}$，它是在反射发生的点处垂直于表面的单位向量；以及表面的特性——颜色、光泽度或者依赖于具体模型的其他属性。

### 4.5.1 Lambertian Shading 朗伯着色

The simplest shading model is based on an observation made by Lambert in the 18th century: the amount of energy from a light source that falls on an area of surface depends on the angle of the surface to the light. A surface facing directly toward the light receives maximum illumination; a surface tangent to the light direction (or facing away from the light) receives no illumination; and in between the illumination is proportional to the cosine of the angle $θ$ between the surface normal and the light source (Figure 4.12). This leads to the Lambertian shading model: 
最简单的着色模型基于18世纪Lambert的一个观察：光源投射到表面区域的能量量取决于表面与光线的角度。正对光源的表面接收到最大的照明；与光线方向相切（或背对光源）的表面不受照明；而在两者之间，照明与表面法线与光源之间的角度$θ$的余弦成正比（见图4.12）。由此产生了Lambertian着色模型：
$L = k_d I max(0, \bold{n} · \bold{l})  $

where $L$ is the pixel color; $k_d$ is the diffuse coefficient, or the surface color; and $I$ is the intensity of the light source. Because $\bold{n}$ and $\bold{l}$ are unit vectors, we can  use $\bold{n} · \bold{l}$ as a convenient shorthand (both on paper and in code) for $\cos θ$. This equation (as with the other shading equations in this section) applies separately to the three color channels, so the red component of the pixel value is the product of the red diffuse component, the red light source intensity, and the dot product; the same holds for green and blue. 
其中，$L$代表像素颜色；$k_d$是漫反射系数，即表面颜色；$I$是光源强度。由于$\bold{n}$和$\bold{l}$是单位向量，我们可以使用$\bold{n} · \bold{l}$作为$\cos θ$的便捷缩写（在纸上和代码中都如此）。这个方程（与本节中的其他着色方程一样）分别应用于三个颜色通道，因此像素值的红色分量是红色漫反射分量、红色光源强度和点积的乘积；绿色和蓝色同理。
![Figure 4.12](.\Images\Figure 4.12.png)
Figure 4.12. Geometry for Lambertian shading.
图 4.12  朗伯着色的几何形状。

> Illumination from real point sources falls off as distance squared, but that is often more trouble than it’s worth in a simple renderer. 
> 真实点光源的照明随距离的平方衰减，然而在简单的渲染器中，这通常带来的麻烦往往超过了其所值。

The vector $\bold{l}$ is computed by subtracting the intersection point of the ray and surface from the light source position. Don’t forget that $\bold{v}$, $\bold{l}$, and $\bold{n}$ all must be unit vectors; failing to normalize these vectors is a very common error in shading computations. 
向量$\bold{l}$通过从射线与表面的交点到光源位置进行减法计算而得。切勿忘记$\bold{v}$、$\bold{l}$和$\bold{n}$都必须是单位向量；在着色计算中未对这些向量进行归一化是一个非常常见的错误。

> When in doubt, make light sources neutral in color, with equal red, green, and blue intensities. 
> 当迷茫时，让光源保持中性颜色，红、绿、蓝三种强度相等。

### 4.5.2 Blinn-Phong Shading Blinn-Phong 着色

Lambertian shading is view independent: the color of a surface does not depend on the direction from which you look. Many real surfaces show some degree of shininess, producing highlights, or specular reflections, that appear to move around as the viewpoint changes. Lambertian shading doesn’t produce any highlights and leads to a very matte, chalky appearance, and many shading models add a specular component to Lambertian shading; the Lambertian part is then the diffuse component. 
Lambertian着色是与视角无关的：表面的颜色不取决于观察的方向。许多真实的表面显示出一定程度的光泽，产生高光或镜面反射，随着视点的变化而呈现出移动的效果。Lambertian着色不会产生任何高光，呈现出一种非常哑光、粉笔般的外观，因此许多着色模型在Lambertian着色基础上添加了镜面成分；而Lambertian部分则是漫反射成分。

A very simple and widely used model for specular highlights was proposed by Phong (Phong, 1975) and later updated by Blinn (J. F. Blinn, 1976) to the form most commonly used today. The idea is to produce reflection that is at its brightest when $\bold{v}$ and $\bold{l}$ are symmetrically positioned across the surface normal, which is when mirror reflection would occur; the reflection then decreases smoothly as the vectors move away from a mirror configuration. 
Phong (Phong, 1975)提出了一个非常简单和广泛使用的镜面高光模型，后来由Blinn (J. F. Blinn, 1976)更新为今天最常用的形式。这个想法是产生最亮的反射，当$\bold{v}$和$\bold{l}$对称地放置在表面法线上，这是镜子反射发生的时候；然后，随着矢量远离镜像配置，反射平滑地减小。

![Figure 4.15](.\Images\Figure 4.15.png)
Figure 4.13. A simple scene rendered with diffuse shading from a single light source. 
图4.13。用来自单一光源的漫反射着色渲染的简单场景。

![Figure 4.14](.\Images\Figure 4.14.png)
Figure 4.14. A simple scene rendered with diffuse shading and shadows (Section 4.7) from three light sources. 
图4.14。用来自三个光源的漫反射着色和阴影（第4.7节)渲染的简单场景。

![Figure 4.13](.\Images\Figure 4.13.png)
Figure 4.15. A simple scene rendered with diffuse shading (blue sphere), Blinn-Phong shading (green sphere), and shadows from three light sources. 
图4.15。用漫反射着色（蓝色球）、Blinn-Phong着色（绿色球)和来自三个光源的阴影渲染的简单场景。

We can tell how close we are to a mirror configuration by comparing the half vector $\bold{h}$ (the bisector of the angle between $\bold{v}$ and $\bold{l}$) to the surface normal (Figure 4.16). If the half vector is near the surface normal, the specular component  should be bright; if it is far away it should be dim. This result is achieved by computing the dot product between $\bold{h}$ and $\bold{n}$ (remember they are unit vectors, so  $\bold{n} · \bold{h}$ reaches its maximum of 1 when the vectors are equal), then taking the result to a power $p > 1$ to make it decrease faster. The power, or Phong exponent, controls the apparent shininess of the surface. The half vector itself is easy to compute: since $\bold{v}$ and $\bold{l}$ are the same length, their sum is a vector that bisects the angle between them, which only needs to be normalized to produce $\bold{h}$. 
通过将半向量$\bold{h}$（$\bold{v}$和$\bold{l}$之间角度的角平分线）与表面法线进行比较，我们可以判断离镜面配置有多近（见图4.16）。如果半向量接近表面法线，那么镜面成分应该较亮；如果远离，则应该较暗。这一结果通过计算$\bold{h}$和$\bold{n}$的点积来实现（请记住它们都是单位向量，因此当向量相等时，$\bold{n} · \bold{h}$达到最大值1），然后将结果取幂$p > 1$以使其更快地减小。幂，或称为Phong指数，控制着表面的明显光泽度。半向量本身很容易计算：由于$\bold{v}$和$\bold{l}$的长度相同，它们的和是一个将它们之间角度平分的向量，只需对其进行归一化即可得到$\bold{h}$。
![Figure 4.16](.\Images\Figure 4.16.png)
Figure 4.16. Geometry for Blinn-Phong shading. 
图 4.16  Blinn-Phong 着色的几何形状。

Putting this all together, the Blinn-Phong shading model is as follows: 
将所有这些放在一起，Blinn-Phong 着色模型如下：
$$
\bold{h} = \frac{\bold{v} + \bold{l}}{\|\bold{v} + \bold{l}\|} \\
L = k_d I max(0, \bold{n} · \bold{l}) + k_s I max(0, \bold{n} · \bold{h})^p
$$
where $k_s$ is the specular coefficient, or the specular color, of the surface. 
其中 $k_s$ 是表面的镜面反射系数或镜面反射颜色。

> Typical values of p:
> 10—“eggshell”;
> 100—mildly shiny;
> 1000—really glossy;
> 10,000—nearly mirror-like. 
> p 的典型值： 10——“蛋壳”； 100——轻微光泽； 1000——非常有光泽； 10,000——几乎像镜子一样。

> When in doubt, make the specular color gray, with equal red, green, and blue values. 
> 如有疑问，请将镜面反射颜色设置为灰色，并具有相同的红色、绿色和蓝色值。

### 4.5.3 Ambient Shading 环境着色

Surfaces that receive no illumination at all will be rendered as completely black, which is often not desirable. A crude but useful heuristic to avoid black shadows  is to add a constant component to the shading model, one whose contribution to the pixel color depends only on the object hit, with no dependence on the surface geometry at all. This is known as ambient shading—it is as if surfaces were illuminated by “ambient” light that comes equally from everywhere. For  convenience in tuning the parameters, ambient shading is usually expressed as the product of a surface color with an ambient light color, so that ambient shading can be tuned for surfaces individually or for all surfaces together. Together with the rest of the Blinn-Phong model, ambient shading completes the full version of a simple and useful shading model:
完全没有受到照明的表面将被渲染为全黑，这通常是不可取的。 避免黑色着色的一种粗略但有用的启发式方法是向着色模型添加一个常量组件，该组件对像素颜色的贡献仅取决于物体击中，而完全不依赖于表面几何形状。 这被称为环境着色——就好像表面被来自各处的“环境”光照亮一样。 为了方便调整参数，环境明暗通常表示为表面颜色与环境光颜色的乘积，以便可以针对单独的表面或针对所有表面一起调整环境明暗。 与 Blinn-Phong 模型的其余部分一起，环境着色完成了简单且有用的着色模型的完整版本：
$$
L = k_aI_a + k_d I max(0, \bold{n} · \bold{l}) + k_s I max(0, \bold{n} · \bold{h})^n, (4.3)
$$
where $k_a$ is the surface’s ambient coefficient, or “ambient color,” and $I_a$ is the  ambient light intensity.
其中 $k_a$ 是表面的环境系数或“环境颜色”，$I_a$ 是环境光强度。

> In the real world, surfaces that are not illuminated by light sources are illuminated by indirect reflections from other surfaces. 
> 在现实世界中，未被光源照亮的表面会被其他表面的间接反射照亮。

> When in doubt set the ambient color to be the same as the diffuse color. ·
> 如果有疑问，请将环境颜色设置为与漫反射颜色相同。

### 4.5.4 Multiple Point Lights  多点光源

A very useful property of light is superposition—the effect caused by more than one light source is simply the sum of the effects of the light sources individually. For this reason, our simple shading model can easily be extended to handle $N$ light sources: 
光的一个非常有用的特性是叠加性——由多个光源引起的效果仅仅是各个光源效果的总和。因此，基于这一原因，我们简单的着色模型可以轻松地扩展以处理$N$个光源：
$$
L = k_a I_a + \sum^N_{i = 1}[k_d I_i max(0, \bold{n} · \bold{l}_i) + k_s I_i max(0, \bold{n} · \bold{h}_i)^p] \ \ \  \ \ (4.4)
$$
where $I_i$, $l_i$, and $h_i$ are the intensity, direction, and half vector of the $i^{th}$ light source. 
其中，$I_i$、$l_i$和$h_i$分别表示第$i$个光源的强度、方向和半向量。



## 4.6 A Ray-Tracing Program 光线追踪程序

We now know how to generate a viewing ray for a given pixel, how to find the closest intersection with an object, and how to shade the resulting intersection. These are all the parts required for a program that produces shaded images with hidden surfaces removed. 
我们现在知道了如何为给定像素生成观察射线，如何找到与物体的最近交点，以及如何着色生成的交点。这些都是生成具有隐藏表面的着色图像所需的所有组成部分。

```lua
for each pixel do
	compute viewing ray
	if (ray hits an object with t ∈ [0, ∞)) then
		Compute n
		Evaluate shading model and set pixel to that color
	else
		set pixel color to background color
```

Here the statement “if ray hits an object . . . ” can be implemented using the algorithm of Section 4.4.4.
这里的陈述“如果光线击中一个物体 . . . ”可以使用4.4.4节的算法来实现。

In an actual implementation, the surface intersection routine needs to somehow return either a reference to the object that is hit, or at least its normal vector and shading-relevant material properties. This is often done by passing a record/structure with such information. In an object-oriented implementation, it is a good idea to have a class called something like surface with derived classes triangle, sphere, group, etc. Anything that a ray can intersect would be under that class. The ray-tracing program would then have one reference to a “surface” for the whole model, and new types of objects and efficiency structures can be added transparently.
在实际的实现中，表面相交例程需要以某种方式返回击中的物体的引用，或者至少返回其法向量和与着色相关的材质属性。通常通过传递包含此类信息的记录/结构来实现。在面向对象的实现中，有一个名为surface的类是一个不错的选择，它可以派生出triangle、sphere、group等类。射线可以相交的任何物体都将属于这个类。然后，射线跟踪程序可以对整个模型引用一个“surface”，而新类型的对象和效率结构可以在其中透明地添加。

### 4.6.1 Object-Oriented Design for a Ray-Tracing Program 光线追踪程序的面向对象设计

As mentioned earlier, the key class hierarchy in a ray tracer are the geometric objects that make up the model. These should be subclasses of some geometric object class, and they should support a hit function (Kirk & Arvo, 1988). To avoid confusion from use of the word “object,” surface is the class name often used. With such a class, you can create a ray tracer that has a general interface that assumes little about modeling primitives and debug it using only spheres. An important point is that anything that can be “hit” by a ray should be part of this class hierarchy, e.g., even a collection of surfaces should be considered a subclass of the surface class. This includes efficiency structures, such as bounding volume hierarchies; they can be hit by a ray, so they are in the class. 
如前所述，在射线追踪器中的关键类层次结构是组成模型的几何对象。这些应该是某个几何对象类的子类，并且它们应该支持一个撞击函数（Kirk & Arvo, 1988）。为了避免使用“对象”一词引起混淆，通常会使用surface作为类名。有了这样一个类，你可以创建一个射线追踪器，它具有一个假定对建模原语了解较少的通用接口，并且只使用球体进行调试。一个重要的观点是，任何可以被射线“击中”的东西都应该是这个类层次结构的一部分，例如，即使是一组表面也应该被视为surface类的子类。这包括效率结构，如包围体层次结构；它们可以被射线击中，因此它们属于这个类。

For example, the “abstract” or “base” class would specify the hit function as well as a bounding box function that will prove useful later: 
例如，“抽象”或“基”类将指定命中函数以及稍后将证明有用的边界框函数：

```python
class surface
	virtual bool hit(ray e + td, real t0, real t1, hit-record rec)
	virtual box bounding-box()
```

Here $(t_0, t_1)$ is the interval on the ray where hits will be returned, and rec is are cord that is passed by reference; it contains data such as the t at the intersection when hit returns true. The type box is a 3D “bounding box,” that is two points that define an axis-aligned box that encloses the surface. For example, for a sphere,t he function would be implemented by 
这里，$(t_0, t_1)$ 表示射线上返回相交的区间，而 rec 是通过引用传递的记录；它包含诸如当 hit 返回 true 时相交处的 t 值等数据。类型 box 是一个3D的“包围盒”，即定义一个轴对齐的盒子的两个点，用于包裹表面。例如，对于一个球体，该函数会被实现为：

```python
box sphere::bounding-box()
	vector3 min = center − vector3(radius,radius,radius)
	vector3 max = center + vector3(radius,radius,radius)
	return box(min, max)
```

Another class that is useful is material. This allows you to abstract the material behavior and later add materials transparently. A simple way to link objects and materials is to add a pointer to a material in the surface class, although more programmable behavior might be desirable. A big question is what to do with textures; are they part of the material class or do they live outside of the material class? This will be discussed more in Chapter 11.
另一个有用的类是材质（material）。这使你能够抽象出材质的行为，并且之后能够透明地添加材质。将对象和材质关联的一种简单方式是在surface类中添加一个指向材质的指针，尽管可能希望有更可编程的行为。一个重要的问题是如何处理纹理；它们是材质类的一部分，还是存在于材质类之外？这将在第11章中进行更详细的讨论。

## 4.7 Shadows 阴影

Once you have a basic ray tracing program, shadows can be added very easily. Recall from Section 4.5 that light comes from some direction $\bold{l}$. If we imagine ourselves at a point $\bold{p}$ on a surface being shaded, the point is in shadow if we “look” in direction $\bold{l}$ and see an object. If there are no objects, then the light is not blocked. 
一旦有了基本的光线追踪程序，就可以非常轻松地添加阴影。 回想一下 4.5 节，光来自某个方向 $\bold{l}$。 如果我们想象自己位于被阴影表面上的一个点 $\bold{p}$ 处，那么如果我们向 $\bold{l}$ 方向“看”并看到一个物体，则该点处于阴影中。 如果没有物体，那么光线就不会被阻挡。

This is shown in Figure 4.17, where the ray $\bold{p} + t\bold{l}$ does not hit any objects and is thus not in shadow. The point $\bold{q}$ is in shadow because the ray $\bold{q} + t\bold{l}$ does hit an object. The vector $\bold{l}$ is the same for both points because the light is “far” away. This assumption will later be relaxed. The rays that determine in or out of shadow are called shadow rays to distinguish them from viewing rays. 
如图 4.17 所示，其中光线 $\bold{p} + t\bold{l}$ 没有击中任何物体，因此不在阴影中。 点 $\bold{q}$ 位于阴影中，因为光线 $\bold{q} + t\bold{l}$ 确实击中了物体。 两个点的向量 $\bold{l}$ 是相同的，因为光距离“很远”。 这个假设稍后会被放宽。 确定阴影内或阴影外的光线称为阴影光线，以区别于观察光线。
![Figure 4.17](.\Images\Figure 4.17.png)
Figure 4.17. The point $\bold{p}$ is not in shadow, while the point $\bold{q}$  is in shadow. 
图 4.17  点 $\bold{p}$ 不在阴影中，而点 $\bold{q}$ 在阴影中

To get the algorithm for shading, we add an if statement to determine whether the point is in shadow. In a naive implementation, the shadow ray will check for $t ∈ [0, ∞)$, but because of numerical imprecision, this can result in an intersection with the surface on which $\bold{p}$ lies. Instead, the usual adjustment to avoid that problem is to test for $t ∈ [\epsilon, ∞)$ where $\epsilon$ is some small positive constant (Figure 4.18). 
为了获得阴影算法，我们添加一个 if 语句来确定该点是否处于阴影中。 在简单的实现中，阴影光线将检查 $t ∈ [0, ∞)$，但由于数值不精确，这可能会导致与 $\bold{p}$ 所在的表面相交。 相反，避免该问题的通常调整是测试 $t ∈ [\epsilon, ∞)$，其中 $\epsilon$ 是一些小的正常数（图 4.18）。
![Figure 4.18](.\Images\Figure 4.18.png)
Figure 4.18. By testing in the interval starting at $\epsilon$, we avoid numerical imprecision causing the ray to hit the surface $\bold{p}$ is on. 
图 4.18  通过在从 $\epsilon$ 开始的间隔中进行测试，我们可以避免数值不精确导致光线撞击 $\bold{p}$ 所在的表面

If we implement shadow rays for Phong lighting with Equation 4.3 then we have the following: 
如果我们使用公式 4.3 实现 Phong 照明的阴影光线，则我们有以下结果：

> **function** raycolor(ray $\bold{e} + t\bold{d}$, real $t_0$, real $t_1$)
> 	hit-record rec, srec
> 	**if** (scene$\rightarrow$hit($\bold{e} + t\bold{d}$, $t_0$, $t_1$, rec)) **then**
> 		$\bold{p} = \bold{e} + (rec.t)\bold{d}$
> 		color c = $rec.k_a I_a$
> 		**if** (not scene $\rightarrow$ hit($\bold{p} + s\bold{l}$, $\epsilon$, $\infty$, srec)) **then**
> 			vector3 **h** = normalized(normalized(**l**) + normalized(-**d**))
> 			c = c + rec.$k_d I$ max($0, rec.\bold{n} \cdot \bold{l}$) + (rec.$k_s$)$I$$(rec.\bold{n} \cdot \bold{h})^{rec.p}$
> 		**return** c
> 	**else**
> 		**return** background-color

Note that the ambient color is added whether $\bold{p}$ is in shadow or not. If there are multiple light sources, we can send a shadow ray before evaluating the shading model for each light. The code above assumes that $\bold{d}$ and $\bold{l}$ are not necessarily unit vectors. This is crucial for $\bold{d}$, in particular, if we wish to cleanly add instancing later (see Section 13.2).
请注意，无论 $\bold{p}$ 是否处于阴影中，都会添加环境颜色。 如果有多个光源，我们可以在评估每个光源的着色模型之前发送阴影光线。 上面的代码假设 $\bold{d}$ 和 $\bold{l}$ 不一定是单位向量。 这对于 $\bold{d}$ 至关重要，特别是如果我们希望稍后干净地添加实例（参见第 13.2 节）。

## 4.8 Ideal Specular Reflection 理想的镜面反射

It is straightforward to add ideal specular reflection, or mirror reflection, to a raytracing program. The key observation is shown in Figure 4.19 where a viewer looking from direction $\bold{e}$ sees what is in direction $\bold{r}$ as seen from the surface. The vector $\bold{r}$ is found using a variant of the Phong lighting reflection Equation (10.6). There are sign changes because the vector $\bold{d}$ points toward the surface in this case, so, 
将理想的镜面反射或镜面反射添加到光线跟踪程序中非常简单。 关键观察结果如图 4.19 所示，其中从 $\bold{e}$ 方向观看的观看者看到的是从表面看到的 $\bold{r}$ 方向的内容。 向量 $\bold{r}$ 是使用 Phong 光照反射方程 (10.6) 的变体找到的。 符号发生变化，因为在这种情况下向量 $\bold{d}$ 指向表面，因此，
$$
\bold{r} = \bold{d} − 2(\bold{d} · \bold{n})\bold{n}. \ \ \ \ (4.5)
$$
![Figure 4.19](.\Images\Figure 4.19.png)
Figure 4.19. When looking into a perfect mirror, the viewer looking in direction $\bold{d}$ will see whatever the viewer “below” the surface would see in direction $\bold{r}$. 
图4.19。当注视一个完美的镜子时，向着方向$\bold{d}$的观察者将看到与表面“下方”观察者在方向$\bold{r}$中所看到的相同。

In the real world, some energy is lost when the light reflects from the surface, and this loss can be different for different colors. For example, gold reflects yellow more efficiently than blue, so it shifts the colors of the objects it reflects. This can be implemented by adding a recursive call in raycolor: 
在现实世界中，当光线从表面反射时会有一些能量损失，而这种损失对不同颜色可能是不同的。例如，金材料比蓝色更有效地反射黄色，因此它会改变所反射对象的颜色。这可以通过在raycolor中添加递归调用来实现：
$color\ c = c + k_m raycolor(\bold{p} + s\bold{r}, \epsilon, ∞)  $

where $k_m$ (for “mirror reflection”) is the specular RGB color. We need to make sure we test for $s ∈ [	\epsilon, ∞)$ for the same reason as we did with shadow rays; we don’t want the reflection ray to hit the object that generates it. 
其中 $k_m$（“镜面反射”）是镜面 RGB 颜色。 我们需要确保测试 $s ∈ [ \epsilon, ∞)$ 的原因与我们测试阴影光线的原因相同； 我们不希望反射光线击中产生它的物体。

The problem with the recursive call above is that it may never terminate. For example, if a ray starts inside a room, it will bounce forever. This can be fixed by adding a maximum recursion depth. The code will be more efficient if a reflection ray is generated only if $k_m$ is not zero (black). 
上述递归调用的问题在于它可能永远不会终止。例如，如果一条射线从房间内开始，它将永远反弹。可以通过添加最大递归深度来解决这个问题。如果$k_m$不为零（黑色），则仅在这种情况下生成反射射线将使代码更加高效。
![Figure 4.20](.\Images\Figure 4.20.png)
Figure 4.20. A simple scene rendered with diffuse and Blinn-Phong shading, shadows from three light sources, and specular reflection from the floor.
图4.20。用漫反射和Blinn-Phong着色、来自三个光源的阴影以及地板的镜面反射渲染的简单场景。

## 4.9 Historical Notes 历史笔记

Ray tracing was developed early in the history of computer graphics (Appel, \1968) but was not used much until sufficient compute power was available (Kay & Greenberg, 1979; Whitted, 1980).
光线追踪是在计算机图形学历史的早期开发的（Appel，\1968），但直到有足够的计算能力才得到广泛使用（Kay & Greenberg，1979；Whitted，1980）。

Ray tracing has a lower asymptotic time complexity than basic object-order rendering (Snyder & Barr, 1987; Muuss, 1995; S. Parker et al., 1999; Wald, Slusallek, Benthin, & Wagner, 2001). Although it was traditionally thought of  as an offline method, real-time ray tracing implementations are becoming more and more common.
光线追踪的渐近时间复杂度低于基本的对象顺序渲染（Snyder & Barr，1987；Muuss，1995；S. Parker 等，1999；Wald、Slusallek、Benthin 和 Wagner，2001）。 尽管传统上它被认为是一种离线方法，但实时光线追踪实现正变得越来越普遍。

## Frequently Asked Questions  经常问的问题

### Why is there no perspective matrix in ray tracing? 为什么光线追踪中没有透视矩阵？

The perspective matrix in a z-buffer exists so that we can turn the perspective projection into a parallel projection. This is not needed in ray tracing, because it is easy to do the perspective projection implicitly by fanning the rays out from the eye.
z 缓冲区中存在透视矩阵，以便我们可以将透视投影转换为平行投影。 这在光线追踪中是不需要的，因为通过将光线从眼睛扇形散开来隐式地进行透视投影很容易。

### Can ray tracing be made interactive? 光线追踪可以交互吗？

For sufficiently small models and images, any modern PC is sufficiently powerful for ray tracing to be interactive. In practice, multiple CPUs with a shared frame buffer are required for a full-screen implementation. Computer power is increasing much faster than screen resolution, and it is just a matter of time before conventional PCs can ray trace complex scenes at screen resolution.
对于足够小的模型和图像，任何现代 PC 都足够强大，可以进行交互式光线追踪。 实际上，全屏实现需要多个具有共享帧缓冲区的 CPU。 计算机能力的增长速度远远快于屏幕分辨率的增长速度，传统 PC 以屏幕分辨率对复杂场景进行光线追踪只是时间问题。

### Is ray tracing useful in a hardware graphics program? 光线追踪在硬件图形程序中有用吗？

Ray tracing is frequently used for picking. When the user clicks the mouse on a pixel in a 3D graphics program, the program needs to determine which object is visible within that pixel. Ray tracing is an ideal way to determine that. 
射线追踪经常用于拾取操作。当用户在3D图形程序中点击鼠标的一个像素时，程序需要确定在该像素内哪个物体是可见的。射线追踪是确定这一点的理想方式。

## Exercises

1. What are the ray parameters of the intersection points between ray $(1, 1, 1)+ t(-1, -1, -1)$ and the sphere centered at the origin with radius 1? Note: this is a good debugging case. 
   射线 $(1, 1, 1)+ t(-1, -1, -1)$ 与以原点为中心、半径为 1 的球体之间的交点的射线参数是多少？ 注意：这是一个很好的调试案例。
2. What are the barycentric coordinates and ray parameter where the ray $(1, 1, 1) + t(-1, -1, -1)$ hits the triangle with vertices $(1, 0, 0)$, $(0, 1, 0)$, and $(0, 0, 1)$? Note: this is a good debugging case. 
   当射线$(1,1,1)+ t(-1， -1， -1)$碰到顶点$(1,0,0)$，$(0,1,0)$和$(0,0,1)$的三角形时，质心坐标和射线参数是什么?注意:这是一个很好的调试案例。
3. Do a back of the envelope computation of the approximate time complexity of ray tracing on “nice” (non-adversarial) models. Split your analysis into the cases of preprocessing and computing the image, so that you can predict the behavior of ray tracing multiple frames for a static model. 
   对“好的”（非对抗性）模型上的光线追踪的近似时间复杂度进行回溯计算。 将您的分析分为预处理和计算图像的情况，以便您可以预测静态模型的光线追踪多帧的行为。